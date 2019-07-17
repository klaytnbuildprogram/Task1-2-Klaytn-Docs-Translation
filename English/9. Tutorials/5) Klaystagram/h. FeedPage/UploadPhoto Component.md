# 7-2. UploadPhoto Component


upload photo
UploadPhoto component's role

Component code

Interact with contract  

Update data to store: updateFeed function

## 1) UploadPhoto component's role
Through UploadPhoto component, we can upload photos to the Klaytn blockchain in the form of NFT(non-fungible-token). To do this, it works as follows: 1. Send transaction by calling uploadPhoto. 2. After sending transaction, show progress with Toast component in trasaction life cycle. 3. When transaction gets into block, update new PhotoData to store.

## 2) Component code
// src/components/UploadPhoto.js
​
import React, { Component } from 'react'
import { connect } from 'react-redux'
import imageCompression from 'utils/imageCompression';
import ui from 'utils/ui'
import Input from 'components/Input'
import InputFile from 'components/InputFile'
import Textarea from 'components/Textarea'
import Button from 'components/Button'
​
import * as photoActions from 'redux/actions/photos'
​
import './UploadPhoto.scss'
​
const MAX_IMAGE_SIZE = 30000 // 30KB
const MAX_IMAGE_SIZE_MB = 0.03 // 30KB
​
class UploadPhoto extends Component {
  state = {
    file: '',
    fileName: '',
    location: '',
    caption: '',
    warningMessage: '',
    isCompressing: false,
  }
​
  handleInputChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value,
    })
  }
​
  handleFileChange = (e) => {
    const file = e.target.files[0]
    /**
     * If image size is bigger than MAX_IMAGE_SIZE(30KB),
     * Compress the image to load it on transaction
     * cf. Maximum transaction input data size: 32KB
     */
    if (file.size > MAX_IMAGE_SIZE) {
      this.setState({
        isCompressing: true,
      })
      return this.compressImage(file)
    }
​
    return this.setState({
      file,
      fileName: file.name,
    })
  }
​
  handleSubmit = (e) => {
    e.preventDefault()
    const { file, fileName, location, caption } = this.state
    this.props.uploadPhoto(file, fileName, location, caption)
    ui.hideModal()
  }
​
  compressImage = async (imageFile) => {
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
​
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
​
const mapDispatchToProps = (dispatch) => ({
  uploadPhoto: (file, fileName, location, caption) =>
    dispatch(photoActions.uploadPhoto(file, fileName, location, caption)),
})
​
export default connect(null, mapDispatchToProps)(UploadPhoto)
## 3) Interact with contract
// src/redux/actions/photo.js
​
export const uploadPhoto = (
  file,
  fileName,
  location,
  caption
) => (dispatch) => {
​
  // 1. Read file's data as an ArrayBuffer
  const reader = new window.FileReader()
  reader.readAsArrayBuffer(file)
  reader.onloadend = () => {
​
    // 2. Convert ArrayBuffer to bytes
    const buffer = Buffer.from(reader.result)
    const bytesString = "0x" + buffer.toString('hex')
​
    // 3. Call contract method(SEND): uploadPhoto
    // Send transaction with bytes of photo image and descriptions
    KlaystagramContract.methods.uploadPhoto(hexString, fileName, location, caption).send({
      from: getWallet().address,
      gas: '20000000',
    })
      .once('transactionHash', (txHash) => {
        // 4. After sending transaction,
        // Show progress with `Toast` component in trasaction life cycle
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
​
        // 5. If transaction successfully gets into block,
        // Call updateFeed function to add new photo data
        const tokenId = receipt.events.PhotoUploaded.returnValues[0]
        dispatch(updateFeed(tokenId))
      })
      .once('error', (error) => {
        ui.showToast({
          status: 'error',
          message: error.toString(),
        })
      })
  }
}
Send transaction to contract: uploadPhoto
We created Contract instance above. Let's make function to write photo data on Klaytn.
Although reading data is free, writing data pays cost for computation & data storage. This cost is called 'gas' and this process is called 'Sending a transaction'.

For these reasons, sending a transaction needs two property from and gas.

Read file's data from UploadPhoto component as an ArrayBuffer using FileReader.

Convert ArrayBuffer to bytes (ArrayBuffer -> hex -> bytes).

Prefix 0x - to satisfy bytes format

Call contract method (SEND): uploadPhoto .

from: account that sends this transaction (= who will pay for this transaction)  

gas: amount of maximum cost willing to pay for sending the transaction

After sending transaction, show progress with Toast component in trasaction life cycle. //@TODO

If transaction success to get into block, Call updateFeed function to add new photo data to feed in store.

cf) Transaction life cycle

After sending transaction, you can get transaction life cycle (transactionHash, receipt, error).

In transactionHash cycle, you can get transaction hash before sending actual transaction.  

In receipt cycle, you can get transaction receipt. It means your transaction got into the block. You can check the block number by receipt.blockNumber.  

In error cycle is triggered when something goes wrong.

## 4. Update data to store: updateFeed
After successfully sending transaction to contract, FeedPage needs to be updated.
In order to update feed we need to get the new photo data we've just uploaded. Let's call getPhoto() with tokenId in receipt that comes right after sending transaction. Then add a new photo data to feed in redux store.

// src/redux/actions/photo.js
​
/**
 * 1. Call contract method (CALL): getPhoto()
 * To get new photo data we've just uploaded,
 * call `getPhoto()` with tokenId from receipt after sending transaction
*/
const updateFeed = (tokenId) => (dispatch, getState) => {
  KlaystagramContract.methods.getPhoto(tokenId).call()
    .then((newPhoto) => {
      const { photos: { feed } } = getState()
      const newFeed = [newPhoto, ...feed]
​
      // 2. update new feed to store
      dispatch(setFeed(newFeed))
    })
}
