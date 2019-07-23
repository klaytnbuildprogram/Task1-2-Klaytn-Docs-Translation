## 7. Feedpage

![FeedPage](./images/klaystagram-feedpage.png)

FeedPage is consisted of 3 main components that interact with `Klaystagram` contract.  

[7-2. `UploadPhoto` component](./7-2-feedpage-uploadphoto.md)  
[7-3. `Feed` component](./7-3-feedpage-feed.md)  
[7-4. `TransferOwnership` component](./7-4-feedpage-transferownership.md)  

```js
// src/pages/FeedPage.js

const FeedPage = () => (
  <main className="FeedPage">
    <UploadButton />               // 7-2. UploadPhoto
    <Feed />                       // 7-3. Feed
  </main>
)
```

```js
// src/components/Feed.js

<div className="Feed">
  {feed.length !== 0
    ? feed.map((photo) => {
      // ...
      return (
        <div className="FeedPhoto" key={id}>
        
            // ...
            {
              userAddress === currentOwner && (
                <TransferOwnershipButton   // 7-4. TransferOwnership
                  className="FeedPhoto__transferOwnership"
                  id={id}
                  issueDate={issueDate}
                  currentOwner={currentOwner}
                />
              )
            }
            // ...
        </div>
      )
    })
    : <span className="Feed__empty">No Photo :D</span>
  }
</div>
)
```

To make component interact with contract, there are 3 steps.

**First**, create `KlaystagramContract` instance to connect contract with front-end. 
**Second**, using `KlaystagramContract` instance, make API functions that interact with contract in `redux/actions`  
**Third**, call functions in each component 

Let's build it!
