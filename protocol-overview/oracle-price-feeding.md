# Oracle Price Feeding

Bend protocol uses NFT floor price from [opensea](http://opensea.io) and [loosrare](https://looksrare.org/) as data of price feeding for NFT collateral. Bend protocol only supports the bluechip NFT asset's floor price for price feeding on-chain. Bluechip NFT's floor price is not easily manipulated. Besides that bend protocol calculate TWAP of floor price to filter the price fluctuate from [opensea](http://opensea.io) and [loosrare](https://looksrare.org/) marketplace.

Bend oracle design and running mechanism:

1. The off-chain node obtains the raw floor price of NFTs from OpenSea and Looksrare trading markets;
2. Filter the raw floor price data, such as the floor price difference between opensea and looksrare is too big;
3. Calculate the floor price according to the transaction volume of opensea and looksrare;
4. Compare the difference between the price on the chain and the latest floor price to determine whether the floor price needs to be uploaded to the chain;
5. Call the contract interface to upload the floor price to the on-chain contract and calculate the time-weighted average price (TWAP) on-chain to weight the floor price, ensuring the price is reasonable;
6. The twap algorithm is open sourced on the on-chain contract, and everyone can verify the validity of the data;

{% hint style="info" %} For cryptopunks ,we get floor price from [CryptoPunksMarket](https://etherscan.io/address/0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb#code) contract!{% endhint %}

![Oracle Mechanism](<../.gitbook/assets/Bend NFT Oracle 0517.png>)

For security and reliability, we will run multiple nodes to ensure that valid price data can be upload to on-chian oracle contract in a timely manner at all times and the  on-chain contract limits the frequency of price feed and the difference between two price feed cannot exceed a threshold.

Bend devs are working with Chainlink team to complete the NFT oracle price feeding.

## Oracle Price Curves

### CryptoPunks Price Curve in 6 months

As shown in the figure, the floor price of the oracle for CryptoPunks is consistent with the average deal price and TWAP price.

![](<../.gitbook/assets/CryptoPunks Price Curve 0401.png>)

### Bored Ape YC Price Curve in 6 months

As shown in the figure, the floor price of the oracle for BAYC is consistent with the average deal price and TWAP price.

![](<../.gitbook/assets/BAYC Price Curve 0401.png>)
