---
title: "Supported Marketplaces"
slug: "supported-marketplaces"
hidden: false
createdAt: "2023-04-21T20:21:44.105Z"
updatedAt: "2023-06-14T02:39:49.136Z"
---
# Marketplaces

Reservoir aggregates both ask and bid liquidity from all major marketplaces. However, due to the various complexities of each protocol, there are some limitations.

| Marketplace      | Listings              | Token Offers          | Collection Offers     | Protocol      |
| :--------------- | :-------------------- | :-------------------- | :-------------------- | :------------ |
| opensea.io       | :white-check-mark:    | :white-check-mark: \* | :white-check-mark:    | Seaport       |
| looksrare.org    | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | LooksRare     |
| x2y2.io          | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | X2Y2          |
| sudoswap.xyz     | :white-check-mark:    | n/a                   | :white-check-mark:    | Sudoswap      |
| nft.coinbase.com | :white-check-mark:    | :white-check-mark:    | n/a                   | 0x v4         |
| rarible.com      | :white-check-mark:    | :x:                   | :white-check-mark:    | Rarible       |
| nftx.io          | :white-check-mark:    | n/a                   | :white-check-mark:    | NFTX          |
| foundation.app   | :white-check-mark:    | :x:                   | n/a                   | Foundation    |
| manifold.xyz     | :white-check-mark:    | n/a                   | n/a                   | Manifold      |
| zora.co          | :white-check-mark:    | :x:                   | :x:                   | Zora Asks 1.1 |
| blur.io          | :white-check-mark: \* | n/a                   | :white-check-mark: \* | Blur          |
| cryptopunks.app  | :white-check-mark:    | :white-check-mark:    | n/a                   | CryptoPunks   |
| element.market   | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Element       |
| infinity.xyz     | :white-check-mark:    | n/a                   | n/a                   | Infinity      |
| universe.xyz     | :white-check-mark:    | n/a                   | n/a                   | Universe      |
| sansa.xyz        | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| ens.vision       | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| magically.gg     | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| alienswap.xyz    | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| sound.xyz        | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| atomic0.com      | :white-check-mark:    | :white-check-mark:    | n/a                   | Seaport       |
| rare.id          | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| parcel.so        | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| metahood.xyz     | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| reservoir.market | :white-check-mark:    | :white-check-mark:    | :white-check-mark:    | Seaport       |
| tessera.co       | :white-check-mark:    | n/a                   | n/a                   | Seaport       |

_\*Due to high volume of spam, only OpenSea token offers within 20% of floor are ingested _  
_\*Blur protocol has some limitations detailed [here](https://docs.reservoir.tools/reference/blur-api#blur-limitations)_

## Market Makers

It's possible for Market Makers to push liquidity directly into Reservoir without an associated marketplace. In those cases, the "source" for the orders will be `reservoir.tools` indicating that they used the Reservoir API. 

## Community Marketplaces

Reservoir also allows community marketplaces to built directly on top of our aggregated order book, either with Reservoir's open-source marketplace UI, or a variety of marketplace-building platforms (e.g. [Snag](https://www.snagsolutions.io/), [FirstMate](https://firstmate.xyz/), [Mobo](https://mobo.xyz/), [PerkShop](https://perk.shop/))

| Community                | Marketplace                      | Built With     |
| :----------------------- | :------------------------------- | :------------- |
| Forgotten Runes          | forgotten.market                 | Custom         |
| GoblinTown               | marketplace.truthlabs.co         | Snag           |
| ApeCoin (Yuga Labs)      | www.apecoinmarketplace.com       | Snag           |
| 9dcc                     | 9dcc.market                      | FirstMate      |
| Bankless                 | market.bankless.com              | FirstMate      |
| SupDucks                 | perk.shop/supducks/shop          | PerkShop       |
| Proof                    | pudding.xyz                      | Mobo           |
| Gmoney                   | gmoney.market                    | Marketplace V1 |
| Finiliar                 | finiliar.com                     | Marketplace V1 |
| Chimpers                 | chimpers.xyz                     | Marketplace V1 |
| GodHatesNFTees           | marketplace.godhatesnftees.com   | Marketplace V1 |
| 6529                     | 6529memes.market                 | Marketplace V1 |
| InBetweeners             | marketplace.inbetweeners.io      | Marketplace V1 |
| Lazy Ape Yacht Club      | marketplace.lazyapeyachtclub.com | Snag           |
| Genuine Undead           | portal.genuineundead.io          | Snag           |
| Boki                     | marketplace.boki.art             | Snag           |
| Los Muertos              | marketplace.los-muertos.io       | Snag           |
| NFTeams                  | marketplace.nfteams.club         | Snag           |
| Pirates of the Metaverse | marketplace.piratesnft.io        | Snag           |
| Zombie Apes              | marketplace.zombieapes.io        | Snag           |
| OnChainBirds             | buy.onchainbirds.com             | Marketplace V1 |
| thric3                   | join.thric3.io                   | Marketplace V1 |
| Dead Birds Society       | underground.deadbirds.io         | Marketplace V1 |
| Milady                   | pleasebepatientwith.me           | FirstMate      |
| Techie Club              | market.techieclub.co             | FirstMate      |
| Bubblegum Kids           | market.bubblegumkids.com         | Marketplace V1 |
| Goldfinch                | lark.market                      | Marketplace V1 |
| Quirkies                 | marketplace.quirkies.io          | Marketplace V1 |
| Eyeverse                 | marketplace.eyeverse.world       | Marketplace V1 |
| Tricil                   | tricil.art                       | Marketplace V1 |
| R Planet                 | marketplace.rplanetnft.xyz       | Snag           |
| Froggy Friends           | marketplace.froggyfriendsnft.com | Snag           |
| Citizens of Tajigen      | marketplace.tajigen.xyz          | Snag           |

## Auctions

Currently, Reservoir only supports _instant_ liquidity. This means we supports fixed priced listings and Dutch Auctions (Seaport only). We don't support English Auctions, however in some cases we still record sales from auctions (see below)

## Sales / Mint Events

In addition to ingesting liquidity, Reservoir parses sale data for the following protocols:

| Marketplace    |
| :------------- |
| ens.domains    |
| artblocks.io   |
| async.art      |
| knownorigin.io |
| okx.com        |
| nouns.wtf      |
| superrare.com  |
| tofunft.com    |
| nfttrader.io   |
| benddao.xyz    |