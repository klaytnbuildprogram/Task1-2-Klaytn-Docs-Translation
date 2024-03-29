## 7-2. UploadPhoto component

![upload photo](./images/klaystagram-uploadphoto.png)

1. `UploadPhoto` component's role
2. Component code
3. Interact with contract  
4. Update data to store: `updateFeed` function

### 1) `UploadPhoto` component's role
`UploadPhoto` component handles the photo upload request to the Klaytn blockchain. The process is as follows:  

1. Invoke `uploadPhoto` method of the smart contract by sending a transaction. Inside the `uploadPhoto` contract method, a new ERC-721 token is minted. 
2. After sending a transaction, show the progress along the transaction life cycle using the `Toast` component.  
3. When the transaction gets into a block, update the new `PhotoData` in the local redux store. 

**Limiting content size**  
The maximum size of a single transaction is `32KB`. So we restrict the input data (photo and descriptions) not to exceed `30KB` to send it over safely.  
- The string data size is restricted to `2KB`
- Photo is compressed to be less than `28KB` using [`imageCompression()`](https://github.com/underbleu/klaystagram/blob/master/src/utils/imageCompression.js) function.

### 2) Component code  

```js
// src/components/UploadPhoto.js

import React, { Component } from 'react'
import { connect } from 'react-redux'
import imageCompression from 'utils/imageCompression';
import ui from 'utils/ui'
import Input from 'components/Input'
import InputFile from 'components/InputFile'
import Textarea from 'components/Textarea'
import Button from 'components/Button'

import * as photoActions from 'redux/actions/photos'

import './UploadPhoto.scss'

// Set a limit of contents
const MAX_IMAGE_SIZE = 28000   // 28KB
const MAX_STRING_SIZE = 2000   // 2KB

class UploadPhoto extends Component {
  state = {
    file: '',
    fileName: '',
    location: '',
    caption: '',
    warningMessage: '',
    isCompressing: false,
  }

  handleInputChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value,
    })
  }

  handleFileChange = (e) => {
    const file = e.target.files[0]

    // If image size is bigger than MAX_IMAGE_SIZE(28KB),
    // Compress the image to load it on transaction
    if (file.size > MAX_IMAGE_SIZE) {
      this.setState({
        isCompressing: true,
      })
      return this.compressImage(file)
    }

    return this.setState({
      file,
      fileName: file.name,
    })
  }

  handleSubmit = (e) => {
    e.preventDefault()
    const { file, fileName, location, caption } = this.state
    this.props.uploadPhoto(file, fileName, location, caption)
    ui.hideModal()
  }

  compressImage = async (imageFile) => {
    const MAX_IMAGE_SIZE_MB = MAX_IMAGE_SIZE / 100000  // 28KB
    try {
      const compressedFile = await imageCompression(imageFile, MAX_IMAGE_SIZE_MB)
      this.setState({
        isCompressing: false,
        file: compressedFile,
        fileName: compressedFile.name,
      })
    } catch (error) {
      this.setState({
        isCompressing: false,
        warningMessage: '* Fail to compress image'
      })
    }
  }

  render() {
    const { fileName, location, caption, isCompressing, warningMessage } = this.state
    return (
      <form className="UploadPhoto" onSubmit={this.handleSubmit}>
        <InputFile
          className="UploadPhoto__file"
          name="file"
          label="Search file"
          fileName={isCompressing ? 'Compressing image...' : fileName}
          onChange={this.handleFileChange}
          err={warningMessage}
          accept=".png, .jpg, .jpeg"
          required
        />
        <Input
          className="UploadPhoto__location"
          name="location"
          label="Location"
          value={location}
          onChange={this.handleInputChange}
          placeholder="Where did you take this photo?"
          required
        />
        <Textarea
          className="UploadPhoto__caption"
          name="caption"
          value={caption}
          label="Caption"
          onChange={this.handleInputChange}
          placeholder="Upload your memories"
          required
        />
        <Button
          className="UploadPhoto__upload"
          type="submit"
          title="Upload"
        />
      </form>
    )
  }
}

const mapDispatchToProps = (dispatch) => ({
  uploadPhoto: (file, fileName, location, caption) =>
    dispatch(photoActions.uploadPhoto(file, fileName, location, caption)),
})

export default connect(null, mapDispatchToProps)(UploadPhoto)
```

### 3) Interact with contract
Let's make a function to write photo data on Klaytn. **Send transaction to contract: `uploadPhoto`**  
Unlike read-only function calls, writing data incurs a transaction fee. The transaction fee is determined by the amount of used `gas`. `gas` is a measuring unit representing how much calculation is needed to process the transaction.

For these reasons, sending a transaction needs two property `from` and `gas`.

1. Convert photo file as a bytes string to load on transaction  
(In [Klaystagram contract](./4-write-smart-contract.md), we defined photo fotmat as bytes in `PhotoData` struct)  
    * Read photo data as an ArrayBuffer using `FileReader`
    * Convert ArrayBuffer to hex string 
    * Add Prefix `0x` to satisfy bytes format  
2. Invoke the contract method: `uploadPhoto`
    * `from`: An account that sends this transaction and pays the transaction fee.  
    * `gas`: The maximum amount of gas that the `from` account is willing to pay for this transaction.
3. After sending the transaction, show progress along the transaction lifecycle using `Toast` component.
4. If the transaction successfully gets into a block, call `updateFeed` function to add the new photo into the feed page.


```js
// src/redux/actions/photo.js

export const uploadPhoto = (
  file,
  fileName,
  location,
  caption
) => (dispatch) => {
  const reader = new window.FileReader()

  // 1. Convert photo file as a hex string to load on transaction
  reader.readAsArrayBuffer(file)
  reader.onloadend = () => {
    const buffer = Buffer.from(reader.result)
    const bytesString = "0x" + buffer.toString('hex')

    // 2. Invoke contract method: uploadPhoto
    // Send transaction with photo file(bytesString) and descriptions
    KlaystagramContract.methods.uploadPhoto(bytesString, fileName, location, caption).send({
      from: getWallet().address,
      gas: '20000000',
    })
      // 3. After sending the transaction,
      // show progress along the transaction lifecycle using `Toast` component.
      .once('transactionHash', (txHash) => {
        ui.showToast({
          status: 'pending',
          message: `Sending a transaction... (uploadPhoto)`,
          txHash,
        })
      })
      .once('receipt', (receipt) => {
        ui.showToast({
          status: receipt.status ? 'success' : 'fail',
          message: `Received receipt! It means your transaction is
          in klaytn block (#${receipt.blockNumber}) (uploadPhoto)`,
          link: receipt.transactionHash,
        })
        
        // 4. If the transaction successfully gets into a block,
        // call `updateFeed` function to add the new photo into the feed page.
        if(receipt.status) {
          const tokenId = receipt.events.PhotoUploaded.returnValues[0]
          dispatch(updateFeed(tokenId))
        }
      })
      .once('error', (error) => {
        ui.showToast({
          status: 'error',
          message: error.toString(),
        })
      })
  }
}
```

**cf) Transaction life cycle**  

After sending transaction, you can get transaction life cycle (`transactionHash`, `receipt`, `error`).  
- `transactionHash` event is fired once your signed transaction instance is properly constructed. You can get the transaction hash before sending the transaction over the network.
- `receipt` event is fired when you get a transaction receipt. It means your transaction is included in a block. You can check the block number by `receipt.blockNumber`.  
- `error` event is fired when something goes wrong.

### 4. Update photo in the feed page: `updateFeed`
After successfully sending the transaction to the contract, FeedPage needs to be updated.  
In order to update the photo feed, we need to get the new photo data we've just uploaded. Let's call `getPhoto()` with `tokenId`. `tokenId` can be retrieved from the transaction receipt. Then add the new photo data in the local redux store. 

```js
// src/redux/actions/photo.js

/**
 * 1. Call contract method: getPhoto()
 * To get new photo data we've just uploaded,
 * call `getPhoto()` with tokenId from receipt after sending transaction
*/
const updateFeed = (tokenId) => (dispatch, getState) => {
  KlaystagramContract.methods.getPhoto(tokenId).call()
    .then((newPhoto) => {
      const { photos: { feed } } = getState()
      const newFeed = [newPhoto, ...feed]
      
      // 2. update new feed to store
      dispatch(setFeed(newFeed))
    })
}
```
