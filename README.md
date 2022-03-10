# Alien Astronaut DJs 
Official Public Codebase  
Check out our [testnet deployment!](https://ropsten.etherscan.io/address/0x759e931a2a2e21C242d907F40ab4B921fE0807f5)
 
## What are Alien Astronaut DJs? 
Alien Astronaut DJs (alasDJs for short) are a collection of 1000 erc-721 NFTs. Each token has a unique image of an alasDJ, as well as an 'instrument' that produces a unique sound. These DJs can be used to generate songs in the [DJ Studio](https://alasdj.com/studio). Songs can be minted as erc-721 tokens that can be traded separately from the alasDJs. Each song is unique and whenever a song is sold on [Opensea](https://opensea.io/) the owners of the DJs used in the song can collect royalties.  
 
## What is in here? 
This codebase contains the smart contracts used for the DJ and song NFTs, as well as the javascript algorithims used to generate the songs. 

## How does the DJ Studio work?
The DJ studio is where you can create songs from alasDJs, start by choosing a DJ and keep pressing mix. Each time mix is pressed, a new 16-byte seed is generated. You can keep pressing this until you hear a beat you like, and then press 'save' in order to save this song. Choose another DJ with an instrument you like and press mix, and it will build on top of the previous one. The algorithim doesn't build entirely random songs, while it can do very random things, it usually mixes songs in a way that will sound good. If you hear a song you like, you can connect to metamask and press 'mint.' Once you confirm the transaction, the song NFT will appear on opensea shortly. 

## How do songs work?
The backbone of the music system is a super-tiny music library called [ZZfx](https://github.com/KilledByAPixel/ZzFX) developed by [Frank Force (KilledByAPixel).](https://twitter.com/KilledByAPixel) Songs are generated in iterations, with each iteration having a DJ that mixes it. A sequence of DJ ids and iteration seeds is created and a song is generated from it. These 2 arrays (ids and seeds) are stored in each song NFT in the smart contract itself. The contract is erc721 with a few extra methods, mint(), and song(). mint() can be called by anyone free of charge, you just need to pay the gas fee. song() can be called by anyone for free, as it just returns the ids and seeds in the token.  
 
Specifically the smart contract function parameters are:  
### mint(bytes ids, bytes seeds)   
WHERE each id is 2 bytes  
WHERE each id can represent decimal 1-1000 (inclusive)  
WHERE each seed is 16 bytes  
WHERE for each id there is a seed (seed.length==bytes.length/8)  
 
=> The id of the new token will be a keccak256 of the dj bytes concatenated with the seed bytes (bytes.concat(ids,seeds)) 
 
### song(tokenID) 
WHERE tokenID is an existing token 
 
=> This function returns 2 byte arrays, ids and seeds respectively 

## How many songs can be created?
Well technically there is no limit to the number of seeds you can keep tacking on, so essentially an infinite amount. Although there are many song combinations(an infinite amount at that) which probably can't be created by this algorithim, infinity-infinity=infinity. 
