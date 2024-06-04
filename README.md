# CoinMarketCap API

![coinmarketcap.png](90c4feb3-a9bf-4f4a-a7b5-f5f48e11c237.png)

Pic source: https://analyticsindiamag.com/guide-to-coinmarketcap-dataset-for-time-series-analysis-historical-prices-of-all-cryptocurrencies/

# Introduction

The Crypto API Project is an automated data collection and analysis tool designed to provide up-to-date information on the top 15 cryptocurrencies by market capitalization. Using the CoinMarketCap API, this project fetches the latest market data at regular intervals and stores it for further analysis.

## Key Features
* **Automated Data Collection:** The project runs continuously, fetching data every four minutes to ensure that the information is always current.

* **Data Storage:** The collected data is stored in a CSV file, enabling easy access and further analysis.

* **Monthly API Call Limit Management:** The project includes logic to manage API call limits, ensuring that it does not exceed the predefined monthly limit of 10,000 calls by CoinMarketCap.


```python
#from API documentation via this link: https://coinmarketcap.com/api/documentation/v1/
#Only want the first 15 cryptocurrencies

from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json

url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
parameters = {
  'start':'1',
  'limit':'15',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': 'YOUR-API',
}

session = Session()
session.headers.update(headers)

try:
  response = session.get(url, params=parameters)
  data = json.loads(response.text)
  print(data)
except (ConnectionError, Timeout, TooManyRedirects) as e:
  print(e)
```

    {'status': {'timestamp': '2024-06-01T15:28:43.658Z', 'error_code': 0, 'error_message': None, 'elapsed': 42, 'credit_count': 1, 'notice': None, 'total_count': 10071}, 'data': [{'id': 1, 'name': 'Bitcoin', 'symbol': 'BTC', 'slug': 'bitcoin', 'num_market_pairs': 11096, 'date_added': '2010-07-13T00:00:00.000Z', 'tags': ['mineable', 'pow', 'sha-256', 'store-of-value', 'state-channel', 'coinbase-ventures-portfolio', 'three-arrows-capital-portfolio', 'polychain-capital-portfolio', 'binance-labs-portfolio', 'blockchain-capital-portfolio', 'boostvc-portfolio', 'cms-holdings-portfolio', 'dcg-portfolio', 'dragonfly-capital-portfolio', 'electric-capital-portfolio', 'fabric-ventures-portfolio', 'framework-ventures-portfolio', 'galaxy-digital-portfolio', 'huobi-capital-portfolio', 'alameda-research-portfolio', 'a16z-portfolio', '1confirmation-portfolio', 'winklevoss-capital-portfolio', 'usv-portfolio', 'placeholder-ventures-portfolio', 'pantera-capital-portfolio', 'multicoin-capital-portfolio', 'paradigm-portfolio', 'bitcoin-ecosystem', 'ftx-bankruptcy-estate'], 'max_supply': 21000000, 'circulating_supply': 19706431, 'total_supply': 19706431, 'infinite_supply': False, 'platform': None, 'cmc_rank': 1, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:26:00.000Z', 'quote': {'USD': {'price': 67711.92323757683, 'volume_24h': 17478298135.435112, 'volume_change_24h': -38.2813, 'percent_change_1h': -0.03089598, 'percent_change_24h': 0.51762976, 'percent_change_7d': -2.08041158, 'percent_change_30d': 14.11703134, 'percent_change_60d': 2.74279713, 'percent_change_90d': 8.80924062, 'market_cap': 1334360343158.6045, 'market_cap_dominance': 52.6547, 'fully_diluted_market_cap': 1421950387989.11, 'tvl': None, 'last_updated': '2024-06-01T15:26:00.000Z'}}}, {'id': 1027, 'name': 'Ethereum', 'symbol': 'ETH', 'slug': 'ethereum', 'num_market_pairs': 9018, 'date_added': '2015-08-07T00:00:00.000Z', 'tags': ['pos', 'smart-contracts', 'ethereum-ecosystem', 'coinbase-ventures-portfolio', 'three-arrows-capital-portfolio', 'polychain-capital-portfolio', 'binance-labs-portfolio', 'blockchain-capital-portfolio', 'boostvc-portfolio', 'cms-holdings-portfolio', 'dcg-portfolio', 'dragonfly-capital-portfolio', 'electric-capital-portfolio', 'fabric-ventures-portfolio', 'framework-ventures-portfolio', 'hashkey-capital-portfolio', 'kenetic-capital-portfolio', 'huobi-capital-portfolio', 'alameda-research-portfolio', 'a16z-portfolio', '1confirmation-portfolio', 'winklevoss-capital-portfolio', 'usv-portfolio', 'placeholder-ventures-portfolio', 'pantera-capital-portfolio', 'multicoin-capital-portfolio', 'paradigm-portfolio', 'injective-ecosystem', 'layer-1', 'ftx-bankruptcy-estate'], 'max_supply': None, 'circulating_supply': 120142090.73330347, 'total_supply': 120142090.73330347, 'infinite_supply': True, 'platform': None, 'cmc_rank': 2, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 3806.8527716482645, 'volume_24h': 11152172057.305702, 'volume_change_24h': -25.7736, 'percent_change_1h': 0.11991459, 'percent_change_24h': 1.04909371, 'percent_change_7d': 1.57448267, 'percent_change_30d': 26.90540955, 'percent_change_60d': 15.50672034, 'percent_change_90d': 11.0214761, 'market_cap': 457363251099.6936, 'market_cap_dominance': 18.052, 'fully_diluted_market_cap': 457363251099.69, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 825, 'name': 'Tether USDt', 'symbol': 'USDT', 'slug': 'tether', 'num_market_pairs': 87491, 'date_added': '2015-02-25T00:00:00.000Z', 'tags': ['stablecoin', 'asset-backed-stablecoin', 'avalanche-ecosystem', 'solana-ecosystem', 'arbitrum-ecosytem', 'moonriver-ecosystem', 'injective-ecosystem', 'bnb-chain', 'usd-stablecoin', 'optimism-ecosystem', 'fiat-stablecoin'], 'max_supply': None, 'circulating_supply': 112141340734.72765, 'total_supply': 115086550406.94923, 'platform': {'id': 1027, 'name': 'Ethereum', 'symbol': 'ETH', 'slug': 'ethereum', 'token_address': '0xdac17f958d2ee523a2206206994597c13d831ec7'}, 'infinite_supply': True, 'cmc_rank': 3, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 0.9991426036532164, 'volume_24h': 42823519461.84376, 'volume_change_24h': -28.4862, 'percent_change_1h': 0.01282979, 'percent_change_24h': -0.00277843, 'percent_change_7d': -0.08081934, 'percent_change_30d': -0.09270636, 'percent_change_60d': -0.09574072, 'percent_change_90d': -0.13026313, 'market_cap': 112045191158.85828, 'market_cap_dominance': 4.4224, 'fully_diluted_market_cap': 114987875619.07, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 1839, 'name': 'BNB', 'symbol': 'BNB', 'slug': 'bnb', 'num_market_pairs': 2173, 'date_added': '2017-07-25T00:00:00.000Z', 'tags': ['marketplace', 'centralized-exchange', 'payments', 'smart-contracts', 'alameda-research-portfolio', 'multicoin-capital-portfolio', 'bnb-chain', 'layer-1', 'sec-security-token', 'alleged-sec-securities', 'celsius-bankruptcy-estate'], 'max_supply': None, 'circulating_supply': 147585277.02826685, 'total_supply': 147585277.02826685, 'infinite_supply': False, 'platform': None, 'cmc_rank': 4, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 597.4037085077657, 'volume_24h': 1475701100.3364832, 'volume_change_24h': -7.965, 'percent_change_1h': 0.15146928, 'percent_change_24h': 0.74702357, 'percent_change_7d': -0.88279047, 'percent_change_30d': 5.71059842, 'percent_change_60d': 7.1287001, 'percent_change_90d': 44.2907123, 'market_cap': 88167991817.83258, 'market_cap_dominance': 3.48, 'fully_diluted_market_cap': 88167991817.83, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 5426, 'name': 'Solana', 'symbol': 'SOL', 'slug': 'solana', 'num_market_pairs': 669, 'date_added': '2020-04-10T00:00:00.000Z', 'tags': ['pos', 'platform', 'solana-ecosystem', 'cms-holdings-portfolio', 'kenetic-capital-portfolio', 'alameda-research-portfolio', 'multicoin-capital-portfolio', 'okx-ventures-portfolio', 'layer-1', 'ftx-bankruptcy-estate', 'sec-security-token', 'alleged-sec-securities', 'cmc-crypto-awards-2024'], 'max_supply': None, 'circulating_supply': 459698026.6221229, 'total_supply': 577256889.5349644, 'infinite_supply': True, 'platform': None, 'cmc_rank': 5, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 167.50743893538618, 'volume_24h': 1496946281.9258385, 'volume_change_24h': -43.1035, 'percent_change_1h': 0.13157364, 'percent_change_24h': 1.02443235, 'percent_change_7d': -0.60552244, 'percent_change_30d': 19.87227302, 'percent_change_60d': -7.789358, 'percent_change_90d': 29.6891161, 'market_cap': 77002839123.12277, 'market_cap_dominance': 3.0393, 'fully_diluted_market_cap': 96694823173.81, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 3408, 'name': 'USDC', 'symbol': 'USDC', 'slug': 'usd-coin', 'num_market_pairs': 19520, 'date_added': '2018-10-08T00:00:00.000Z', 'tags': ['medium-of-exchange', 'stablecoin', 'asset-backed-stablecoin', 'coinbase-ventures-portfolio', 'hedera-hashgraph-ecosystem', 'fantom-ecosystem', 'arbitrum-ecosytem', 'moonriver-ecosystem', 'bnb-chain', 'usd-stablecoin', 'optimism-ecosystem', 'fiat-stablecoin'], 'max_supply': None, 'circulating_supply': 32368833685.309906, 'total_supply': 32368833685.309906, 'platform': {'id': 1027, 'name': 'Ethereum', 'symbol': 'ETH', 'slug': 'ethereum', 'token_address': '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48'}, 'infinite_supply': False, 'cmc_rank': 6, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 1.000222946392991, 'volume_24h': 4159817098.207451, 'volume_change_24h': -32.8365, 'percent_change_1h': 0.01312637, 'percent_change_24h': 0.01435991, 'percent_change_7d': 0.01802717, 'percent_change_30d': 0.01437005, 'percent_change_60d': 0.01854437, 'percent_change_90d': 0.03787023, 'market_cap': 32376050200.02537, 'market_cap_dominance': 1.2779, 'fully_diluted_market_cap': 32376050200.03, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 52, 'name': 'XRP', 'symbol': 'XRP', 'slug': 'xrp', 'num_market_pairs': 1333, 'date_added': '2013-08-04T00:00:00.000Z', 'tags': ['medium-of-exchange', 'enterprise-solutions', 'arrington-xrp-capital-portfolio', 'galaxy-digital-portfolio', 'a16z-portfolio', 'pantera-capital-portfolio', 'ftx-bankruptcy-estate'], 'max_supply': 100000000000, 'circulating_supply': 55450358947, 'total_supply': 99987572899, 'infinite_supply': False, 'platform': None, 'cmc_rank': 7, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:26:00.000Z', 'quote': {'USD': {'price': 0.520815532602451, 'volume_24h': 707848101.0686182, 'volume_change_24h': -42.1003, 'percent_change_1h': -0.05713069, 'percent_change_24h': -0.0338031, 'percent_change_7d': -3.86836214, 'percent_change_30d': -0.11547758, 'percent_change_60d': -11.78707809, 'percent_change_90d': -16.36778732, 'market_cap': 28879408227.978886, 'market_cap_dominance': 1.1399, 'fully_diluted_market_cap': 52081553260.25, 'tvl': None, 'last_updated': '2024-06-01T15:26:00.000Z'}}}, {'id': 74, 'name': 'Dogecoin', 'symbol': 'DOGE', 'slug': 'dogecoin', 'num_market_pairs': 975, 'date_added': '2013-12-15T00:00:00.000Z', 'tags': ['mineable', 'pow', 'scrypt', 'medium-of-exchange', 'memes', 'payments', 'doggone-doggerel', 'bnb-chain', 'ftx-bankruptcy-estate'], 'max_supply': None, 'circulating_supply': 144530506383.7052, 'total_supply': 144530506383.7052, 'infinite_supply': True, 'platform': None, 'cmc_rank': 8, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:26:00.000Z', 'quote': {'USD': {'price': 0.1605148335911048, 'volume_24h': 706069348.5236803, 'volume_change_24h': -34.4427, 'percent_change_1h': -0.2472433, 'percent_change_24h': 0.99010181, 'percent_change_7d': -4.69421144, 'percent_change_30d': 20.10934257, 'percent_change_60d': -14.07694406, 'percent_change_90d': 15.19927133, 'market_cap': 23199290181.01855, 'market_cap_dominance': 0.9157, 'fully_diluted_market_cap': 23199290181.02, 'tvl': None, 'last_updated': '2024-06-01T15:26:00.000Z'}}}, {'id': 2010, 'name': 'Cardano', 'symbol': 'ADA', 'slug': 'cardano', 'num_market_pairs': 1189, 'date_added': '2017-10-01T00:00:00.000Z', 'tags': ['dpos', 'pos', 'platform', 'research', 'smart-contracts', 'staking', 'cardano-ecosystem', 'cardano', 'layer-1', 'sec-security-token', 'alleged-sec-securities'], 'max_supply': 45000000000, 'circulating_supply': 35700460169.947, 'total_supply': 36925434173.444, 'infinite_supply': False, 'platform': None, 'cmc_rank': 9, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 0.4495830613296638, 'volume_24h': 207712400.41250786, 'volume_change_24h': -29.3576, 'percent_change_1h': -0.02405294, 'percent_change_24h': -0.23141596, 'percent_change_7d': -2.44811646, 'percent_change_30d': -2.21518146, 'percent_change_60d': -23.65256746, 'percent_change_90d': -38.03709513, 'market_cap': 16050322174.0825, 'market_cap_dominance': 0.6335, 'fully_diluted_market_cap': 20231237759.83, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 11419, 'name': 'Toncoin', 'symbol': 'TON', 'slug': 'toncoin', 'num_market_pairs': 382, 'date_added': '2021-08-26T13:40:22.000Z', 'tags': ['pos', 'layer-1', 'ftx-bankruptcy-estate', 'dwf-labs-portfolio', 'toncoin-ecosystem'], 'max_supply': None, 'circulating_supply': 2412328696.044575, 'total_supply': 5107159891.962288, 'infinite_supply': True, 'platform': None, 'cmc_rank': 10, 'self_reported_circulating_supply': 3414166606, 'self_reported_market_cap': 21501879738.454178, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 6.297841382628232, 'volume_24h': 129753301.91221951, 'volume_change_24h': -9.1796, 'percent_change_1h': -0.11836245, 'percent_change_24h': -1.59719069, 'percent_change_7d': -2.31268899, 'percent_change_30d': 25.92978163, 'percent_change_60d': 25.23962363, 'percent_change_90d': 137.71725519, 'market_cap': 15192463490.451128, 'market_cap_dominance': 0.5996, 'fully_diluted_market_cap': 32164082915.3, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 5994, 'name': 'Shiba Inu', 'symbol': 'SHIB', 'slug': 'shiba-inu', 'num_market_pairs': 828, 'date_added': '2020-08-01T00:00:00.000Z', 'tags': ['memes', 'ethereum-ecosystem', 'doggone-doggerel'], 'max_supply': None, 'circulating_supply': 589271829576220.8, 'total_supply': 589519966647077.9, 'platform': {'id': 1027, 'name': 'Ethereum', 'symbol': 'ETH', 'slug': 'ethereum', 'token_address': '0x95ad61b0a150d79219dcf64e1e6cc01f0b64c4ce'}, 'infinite_supply': False, 'cmc_rank': 11, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 2.5417521204202936e-05, 'volume_24h': 387563651.44852966, 'volume_change_24h': -41.3246, 'percent_change_1h': 0.21736102, 'percent_change_24h': -0.99382844, 'percent_change_7d': 2.20325562, 'percent_change_30d': 9.57716374, 'percent_change_60d': -4.50185937, 'percent_change_90d': 17.85615305, 'market_cap': 14977829223.293049, 'market_cap_dominance': 0.5912, 'fully_diluted_market_cap': 14984136252.55, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 5805, 'name': 'Avalanche', 'symbol': 'AVAX', 'slug': 'avalanche', 'num_market_pairs': 735, 'date_added': '2020-07-13T00:00:00.000Z', 'tags': ['defi', 'smart-contracts', 'three-arrows-capital-portfolio', 'polychain-capital-portfolio', 'avalanche-ecosystem', 'cms-holdings-portfolio', 'dragonfly-capital-portfolio', 'moonriver-ecosystem', 'injective-ecosystem', 'real-world-assets', 'layer-1'], 'max_supply': 715748719, 'circulating_supply': 393109862.0421839, 'total_supply': 442456232.0421839, 'infinite_supply': False, 'platform': None, 'cmc_rank': 12, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 36.06834437287699, 'volume_24h': 202804903.67799652, 'volume_change_24h': -35.1733, 'percent_change_1h': -0.15759854, 'percent_change_24h': 0.55621077, 'percent_change_7d': -5.62729584, 'percent_change_30d': 6.00560191, 'percent_change_60d': -24.48684583, 'percent_change_90d': -15.66983255, 'market_cap': 14178821880.511654, 'market_cap_dominance': 0.5596, 'fully_diluted_market_cap': 25815871281.34, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 1975, 'name': 'Chainlink', 'symbol': 'LINK', 'slug': 'chainlink', 'num_market_pairs': 1787, 'date_added': '2017-09-20T00:00:00.000Z', 'tags': ['platform', 'defi', 'oracles', 'smart-contracts', 'substrate', 'polkadot', 'polkadot-ecosystem', 'avalanche-ecosystem', 'solana-ecosystem', 'framework-ventures-portfolio', 'polygon-ecosystem', 'fantom-ecosystem', 'cardano-ecosystem', 'web3', 'near-protocol-ecosystem', 'arbitrum-ecosytem', 'cardano', 'injective-ecosystem', 'optimism-ecosystem', 'real-world-assets', 'celsius-bankruptcy-estate'], 'max_supply': 1000000000, 'circulating_supply': 587099970.4527867, 'total_supply': 1000000000, 'platform': {'id': 1027, 'name': 'Ethereum', 'symbol': 'ETH', 'slug': 'ethereum', 'token_address': '0x514910771af9ca656af840dff83e8264ecf986ca'}, 'infinite_supply': False, 'cmc_rank': 13, 'self_reported_circulating_supply': None, 'self_reported_market_cap': None, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 18.608232610892664, 'volume_24h': 386488486.77302194, 'volume_change_24h': -2.8269, 'percent_change_1h': 0.30017191, 'percent_change_24h': 4.95020873, 'percent_change_7d': 8.47663287, 'percent_change_30d': 36.54258179, 'percent_change_60d': 3.83520218, 'percent_change_90d': -9.24408053, 'market_cap': 10924892816.033665, 'market_cap_dominance': 0.4312, 'fully_diluted_market_cap': 18608232610.89, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}, {'id': 6636, 'name': 'Polkadot', 'symbol': 'DOT', 'slug': 'polkadot-new', 'num_market_pairs': 774, 'date_added': '2020-08-19T00:00:00.000Z', 'tags': ['substrate', 'polkadot', 'binance-chain', 'polkadot-ecosystem', 'three-arrows-capital-portfolio', 'polychain-capital-portfolio', 'arrington-xrp-capital-portfolio', 'blockchain-capital-portfolio', 'boostvc-portfolio', 'cms-holdings-portfolio', 'coinfund-portfolio', 'fabric-ventures-portfolio', 'fenbushi-capital-portfolio', 'hashkey-capital-portfolio', 'kenetic-capital-portfolio', '1confirmation-portfolio', 'placeholder-ventures-portfolio', 'pantera-capital-portfolio', 'exnetwork-capital-portfolio', 'web3', 'spartan-group', 'injective-ecosystem', 'bnb-chain', 'layer-1'], 'max_supply': None, 'circulating_supply': 1437953431.368154, 'total_supply': 1437953431.368154, 'infinite_supply': True, 'platform': None, 'cmc_rank': 14, 'self_reported_circulating_supply': 1451892807.902116, 'self_reported_market_cap': 10324245443.935543, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:26:00.000Z', 'quote': {'USD': {'price': 7.11088682838326, 'volume_24h': 145208886.6310823, 'volume_change_24h': -20.6544, 'percent_change_1h': -0.12722433, 'percent_change_24h': 2.50331212, 'percent_change_7d': -3.02092075, 'percent_change_30d': 0.91402363, 'percent_change_60d': -17.10919786, 'percent_change_90d': -23.54201292, 'market_cap': 10225124114.944319, 'market_cap_dominance': 0.4036, 'fully_diluted_market_cap': 10225124114.94, 'tvl': None, 'last_updated': '2024-06-01T15:26:00.000Z'}}}, {'id': 1958, 'name': 'TRON', 'symbol': 'TRX', 'slug': 'tron', 'num_market_pairs': 985, 'date_added': '2017-09-13T00:00:00.000Z', 'tags': ['media', 'payments', 'tron-ecosystem', 'layer-1', 'dwf-labs-portfolio', 'sec-security-token', 'alleged-sec-securities'], 'max_supply': None, 'circulating_supply': 87371139931.27109, 'total_supply': 87371213858.83676, 'infinite_supply': True, 'platform': None, 'cmc_rank': 15, 'self_reported_circulating_supply': 71659659264, 'self_reported_market_cap': 8031750864.145509, 'tvl_ratio': None, 'last_updated': '2024-06-01T15:25:00.000Z', 'quote': {'USD': {'price': 0.11208190140223646, 'volume_24h': 203331542.773364, 'volume_change_24h': -25.7233, 'percent_change_1h': 0.14881163, 'percent_change_24h': 0.19124614, 'percent_change_7d': -1.25053266, 'percent_change_30d': -9.02027546, 'percent_change_60d': -3.85331919, 'percent_change_90d': -20.0525728, 'market_cap': 9792723491.17773, 'market_cap_dominance': 0.3865, 'fully_diluted_market_cap': 9792731777.12, 'tvl': None, 'last_updated': '2024-06-01T15:25:00.000Z'}}}]}
    


```python
type(data)
```




    dict




```python
import pandas as pd

pd.set_option('display.max_columns', None)
```


```python
df = pd.json_normalize(data['data'])
df['timestamp'] = pd.to_datetime('now')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>symbol</th>
      <th>slug</th>
      <th>num_market_pairs</th>
      <th>date_added</th>
      <th>tags</th>
      <th>max_supply</th>
      <th>circulating_supply</th>
      <th>total_supply</th>
      <th>infinite_supply</th>
      <th>platform</th>
      <th>cmc_rank</th>
      <th>self_reported_circulating_supply</th>
      <th>self_reported_market_cap</th>
      <th>tvl_ratio</th>
      <th>last_updated</th>
      <th>quote.USD.price</th>
      <th>quote.USD.volume_24h</th>
      <th>quote.USD.volume_change_24h</th>
      <th>quote.USD.percent_change_1h</th>
      <th>quote.USD.percent_change_24h</th>
      <th>quote.USD.percent_change_7d</th>
      <th>quote.USD.percent_change_30d</th>
      <th>quote.USD.percent_change_60d</th>
      <th>quote.USD.percent_change_90d</th>
      <th>quote.USD.market_cap</th>
      <th>quote.USD.market_cap_dominance</th>
      <th>quote.USD.fully_diluted_market_cap</th>
      <th>quote.USD.tvl</th>
      <th>quote.USD.last_updated</th>
      <th>platform.id</th>
      <th>platform.name</th>
      <th>platform.symbol</th>
      <th>platform.slug</th>
      <th>platform.token_address</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bitcoin</td>
      <td>BTC</td>
      <td>bitcoin</td>
      <td>11096</td>
      <td>2010-07-13T00:00:00.000Z</td>
      <td>[mineable, pow, sha-256, store-of-value, state...</td>
      <td>2.100000e+07</td>
      <td>1.970643e+07</td>
      <td>1.970643e+07</td>
      <td>False</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>67711.923238</td>
      <td>1.747830e+10</td>
      <td>-38.2813</td>
      <td>-0.030896</td>
      <td>0.517630</td>
      <td>-2.080412</td>
      <td>14.117031</td>
      <td>2.742797</td>
      <td>8.809241</td>
      <td>1.334360e+12</td>
      <td>52.6547</td>
      <td>1.421950e+12</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1027</td>
      <td>Ethereum</td>
      <td>ETH</td>
      <td>ethereum</td>
      <td>9018</td>
      <td>2015-08-07T00:00:00.000Z</td>
      <td>[pos, smart-contracts, ethereum-ecosystem, coi...</td>
      <td>NaN</td>
      <td>1.201421e+08</td>
      <td>1.201421e+08</td>
      <td>True</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>3806.852772</td>
      <td>1.115217e+10</td>
      <td>-25.7736</td>
      <td>0.119915</td>
      <td>1.049094</td>
      <td>1.574483</td>
      <td>26.905410</td>
      <td>15.506720</td>
      <td>11.021476</td>
      <td>4.573633e+11</td>
      <td>18.0520</td>
      <td>4.573633e+11</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>2</th>
      <td>825</td>
      <td>Tether USDt</td>
      <td>USDT</td>
      <td>tether</td>
      <td>87491</td>
      <td>2015-02-25T00:00:00.000Z</td>
      <td>[stablecoin, asset-backed-stablecoin, avalanch...</td>
      <td>NaN</td>
      <td>1.121413e+11</td>
      <td>1.150866e+11</td>
      <td>True</td>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>0.999143</td>
      <td>4.282352e+10</td>
      <td>-28.4862</td>
      <td>0.012830</td>
      <td>-0.002778</td>
      <td>-0.080819</td>
      <td>-0.092706</td>
      <td>-0.095741</td>
      <td>-0.130263</td>
      <td>1.120452e+11</td>
      <td>4.4224</td>
      <td>1.149879e+11</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>1027.0</td>
      <td>Ethereum</td>
      <td>ETH</td>
      <td>ethereum</td>
      <td>0xdac17f958d2ee523a2206206994597c13d831ec7</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1839</td>
      <td>BNB</td>
      <td>BNB</td>
      <td>bnb</td>
      <td>2173</td>
      <td>2017-07-25T00:00:00.000Z</td>
      <td>[marketplace, centralized-exchange, payments, ...</td>
      <td>NaN</td>
      <td>1.475853e+08</td>
      <td>1.475853e+08</td>
      <td>False</td>
      <td>NaN</td>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>597.403709</td>
      <td>1.475701e+09</td>
      <td>-7.9650</td>
      <td>0.151469</td>
      <td>0.747024</td>
      <td>-0.882790</td>
      <td>5.710598</td>
      <td>7.128700</td>
      <td>44.290712</td>
      <td>8.816799e+10</td>
      <td>3.4800</td>
      <td>8.816799e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5426</td>
      <td>Solana</td>
      <td>SOL</td>
      <td>solana</td>
      <td>669</td>
      <td>2020-04-10T00:00:00.000Z</td>
      <td>[pos, platform, solana-ecosystem, cms-holdings...</td>
      <td>NaN</td>
      <td>4.596980e+08</td>
      <td>5.772569e+08</td>
      <td>True</td>
      <td>NaN</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>167.507439</td>
      <td>1.496946e+09</td>
      <td>-43.1035</td>
      <td>0.131574</td>
      <td>1.024432</td>
      <td>-0.605522</td>
      <td>19.872273</td>
      <td>-7.789358</td>
      <td>29.689116</td>
      <td>7.700284e+10</td>
      <td>3.0393</td>
      <td>9.669482e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3408</td>
      <td>USDC</td>
      <td>USDC</td>
      <td>usd-coin</td>
      <td>19520</td>
      <td>2018-10-08T00:00:00.000Z</td>
      <td>[medium-of-exchange, stablecoin, asset-backed-...</td>
      <td>NaN</td>
      <td>3.236883e+10</td>
      <td>3.236883e+10</td>
      <td>False</td>
      <td>NaN</td>
      <td>6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>1.000223</td>
      <td>4.159817e+09</td>
      <td>-32.8365</td>
      <td>0.013126</td>
      <td>0.014360</td>
      <td>0.018027</td>
      <td>0.014370</td>
      <td>0.018544</td>
      <td>0.037870</td>
      <td>3.237605e+10</td>
      <td>1.2779</td>
      <td>3.237605e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>1027.0</td>
      <td>Ethereum</td>
      <td>ETH</td>
      <td>ethereum</td>
      <td>0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>6</th>
      <td>52</td>
      <td>XRP</td>
      <td>XRP</td>
      <td>xrp</td>
      <td>1333</td>
      <td>2013-08-04T00:00:00.000Z</td>
      <td>[medium-of-exchange, enterprise-solutions, arr...</td>
      <td>1.000000e+11</td>
      <td>5.545036e+10</td>
      <td>9.998757e+10</td>
      <td>False</td>
      <td>NaN</td>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>0.520816</td>
      <td>7.078481e+08</td>
      <td>-42.1003</td>
      <td>-0.057131</td>
      <td>-0.033803</td>
      <td>-3.868362</td>
      <td>-0.115478</td>
      <td>-11.787078</td>
      <td>-16.367787</td>
      <td>2.887941e+10</td>
      <td>1.1399</td>
      <td>5.208155e+10</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>7</th>
      <td>74</td>
      <td>Dogecoin</td>
      <td>DOGE</td>
      <td>dogecoin</td>
      <td>975</td>
      <td>2013-12-15T00:00:00.000Z</td>
      <td>[mineable, pow, scrypt, medium-of-exchange, me...</td>
      <td>NaN</td>
      <td>1.445305e+11</td>
      <td>1.445305e+11</td>
      <td>True</td>
      <td>NaN</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>0.160515</td>
      <td>7.060693e+08</td>
      <td>-34.4427</td>
      <td>-0.247243</td>
      <td>0.990102</td>
      <td>-4.694211</td>
      <td>20.109343</td>
      <td>-14.076944</td>
      <td>15.199271</td>
      <td>2.319929e+10</td>
      <td>0.9157</td>
      <td>2.319929e+10</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2010</td>
      <td>Cardano</td>
      <td>ADA</td>
      <td>cardano</td>
      <td>1189</td>
      <td>2017-10-01T00:00:00.000Z</td>
      <td>[dpos, pos, platform, research, smart-contract...</td>
      <td>4.500000e+10</td>
      <td>3.570046e+10</td>
      <td>3.692543e+10</td>
      <td>False</td>
      <td>NaN</td>
      <td>9</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>0.449583</td>
      <td>2.077124e+08</td>
      <td>-29.3576</td>
      <td>-0.024053</td>
      <td>-0.231416</td>
      <td>-2.448116</td>
      <td>-2.215181</td>
      <td>-23.652567</td>
      <td>-38.037095</td>
      <td>1.605032e+10</td>
      <td>0.6335</td>
      <td>2.023124e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>9</th>
      <td>11419</td>
      <td>Toncoin</td>
      <td>TON</td>
      <td>toncoin</td>
      <td>382</td>
      <td>2021-08-26T13:40:22.000Z</td>
      <td>[pos, layer-1, ftx-bankruptcy-estate, dwf-labs...</td>
      <td>NaN</td>
      <td>2.412329e+09</td>
      <td>5.107160e+09</td>
      <td>True</td>
      <td>NaN</td>
      <td>10</td>
      <td>3.414167e+09</td>
      <td>2.150188e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>6.297841</td>
      <td>1.297533e+08</td>
      <td>-9.1796</td>
      <td>-0.118362</td>
      <td>-1.597191</td>
      <td>-2.312689</td>
      <td>25.929782</td>
      <td>25.239624</td>
      <td>137.717255</td>
      <td>1.519246e+10</td>
      <td>0.5996</td>
      <td>3.216408e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5994</td>
      <td>Shiba Inu</td>
      <td>SHIB</td>
      <td>shiba-inu</td>
      <td>828</td>
      <td>2020-08-01T00:00:00.000Z</td>
      <td>[memes, ethereum-ecosystem, doggone-doggerel]</td>
      <td>NaN</td>
      <td>5.892718e+14</td>
      <td>5.895200e+14</td>
      <td>False</td>
      <td>NaN</td>
      <td>11</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>0.000025</td>
      <td>3.875637e+08</td>
      <td>-41.3246</td>
      <td>0.217361</td>
      <td>-0.993828</td>
      <td>2.203256</td>
      <td>9.577164</td>
      <td>-4.501859</td>
      <td>17.856153</td>
      <td>1.497783e+10</td>
      <td>0.5912</td>
      <td>1.498414e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>1027.0</td>
      <td>Ethereum</td>
      <td>ETH</td>
      <td>ethereum</td>
      <td>0x95ad61b0a150d79219dcf64e1e6cc01f0b64c4ce</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5805</td>
      <td>Avalanche</td>
      <td>AVAX</td>
      <td>avalanche</td>
      <td>735</td>
      <td>2020-07-13T00:00:00.000Z</td>
      <td>[defi, smart-contracts, three-arrows-capital-p...</td>
      <td>7.157487e+08</td>
      <td>3.931099e+08</td>
      <td>4.424562e+08</td>
      <td>False</td>
      <td>NaN</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>36.068344</td>
      <td>2.028049e+08</td>
      <td>-35.1733</td>
      <td>-0.157599</td>
      <td>0.556211</td>
      <td>-5.627296</td>
      <td>6.005602</td>
      <td>-24.486846</td>
      <td>-15.669833</td>
      <td>1.417882e+10</td>
      <td>0.5596</td>
      <td>2.581587e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1975</td>
      <td>Chainlink</td>
      <td>LINK</td>
      <td>chainlink</td>
      <td>1787</td>
      <td>2017-09-20T00:00:00.000Z</td>
      <td>[platform, defi, oracles, smart-contracts, sub...</td>
      <td>1.000000e+09</td>
      <td>5.871000e+08</td>
      <td>1.000000e+09</td>
      <td>False</td>
      <td>NaN</td>
      <td>13</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>18.608233</td>
      <td>3.864885e+08</td>
      <td>-2.8269</td>
      <td>0.300172</td>
      <td>4.950209</td>
      <td>8.476633</td>
      <td>36.542582</td>
      <td>3.835202</td>
      <td>-9.244081</td>
      <td>1.092489e+10</td>
      <td>0.4312</td>
      <td>1.860823e+10</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>1027.0</td>
      <td>Ethereum</td>
      <td>ETH</td>
      <td>ethereum</td>
      <td>0x514910771af9ca656af840dff83e8264ecf986ca</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>13</th>
      <td>6636</td>
      <td>Polkadot</td>
      <td>DOT</td>
      <td>polkadot-new</td>
      <td>774</td>
      <td>2020-08-19T00:00:00.000Z</td>
      <td>[substrate, polkadot, binance-chain, polkadot-...</td>
      <td>NaN</td>
      <td>1.437953e+09</td>
      <td>1.437953e+09</td>
      <td>True</td>
      <td>NaN</td>
      <td>14</td>
      <td>1.451893e+09</td>
      <td>1.032425e+10</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>7.110887</td>
      <td>1.452089e+08</td>
      <td>-20.6544</td>
      <td>-0.127224</td>
      <td>2.503312</td>
      <td>-3.020921</td>
      <td>0.914024</td>
      <td>-17.109198</td>
      <td>-23.542013</td>
      <td>1.022512e+10</td>
      <td>0.4036</td>
      <td>1.022512e+10</td>
      <td>None</td>
      <td>2024-06-01T15:26:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1958</td>
      <td>TRON</td>
      <td>TRX</td>
      <td>tron</td>
      <td>985</td>
      <td>2017-09-13T00:00:00.000Z</td>
      <td>[media, payments, tron-ecosystem, layer-1, dwf...</td>
      <td>NaN</td>
      <td>8.737114e+10</td>
      <td>8.737121e+10</td>
      <td>True</td>
      <td>NaN</td>
      <td>15</td>
      <td>7.165966e+10</td>
      <td>8.031751e+09</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>0.112082</td>
      <td>2.033315e+08</td>
      <td>-25.7233</td>
      <td>0.148812</td>
      <td>0.191246</td>
      <td>-1.250533</td>
      <td>-9.020275</td>
      <td>-3.853319</td>
      <td>-20.052573</td>
      <td>9.792723e+09</td>
      <td>0.3865</td>
      <td>9.792732e+09</td>
      <td>None</td>
      <td>2024-06-01T15:25:00.000Z</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2024-06-01 17:29:05.658207</td>
    </tr>
  </tbody>
</table>
</div>



# Data Fetching Process
The data is retrieved from the CoinMarketCap API, which provides detailed and current information on various cryptocurrencies. The project uses the `requests` library in Python to send API requests and handle responses. Here's a brief overview of the data fetching and storage process:

1. **API Endpoint:** The project accesses the CoinMarketCap API endpoint for the latest cryptocurrency listings.

2. **Parameters:** The API request is configured to fetch data for the top 15 cryptocurrencies, with prices converted to USD.

3. **Headers:** The request includes the necessary API key for authentication.

4. **Session Management:** A session is created to manage and streamline the API requests.

5. **Error Handling:** The project includes error handling for potential issues such as connection errors, timeouts, and too many redirects.

The fetched data includes various attributes of each cryptocurrency, such as current price, market capitalization, 24-hour trading volume, and more. This data is then can be processed and visualized to provide meaningful insights.



```python
import os
from time import sleep
import datetime
from requests import Session, ConnectionError, Timeout, TooManyRedirects

# Define the monthly limit and initialize the call counter
MONTHLY_LIMIT = 10000
calls_made = 0

def api_runner():
    url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
    parameters = {
        'start': '1',
        'limit': '15',
        'convert': 'USD'
    }
    headers = {
        'Accepts': 'application/json',
        'X-CMC_PRO_API_KEY': 'YOUR-API',
    }
    
    session = Session()
    session.headers.update(headers)
    
    try:
        response = session.get(url, params=parameters)
        data = json.loads(response.text)
        print(data)  # Print the data if needed for debugging
    except (ConnectionError, Timeout, TooManyRedirects) as e:
        print(e)
        return

    # Convert JSON data to DataFrame
    df = pd.json_normalize(data['data'])
    # Add a timestamp
    df['timestamp'] = pd.to_datetime('now')
    
    # Append the DataFrame to a CSV file
    if not os.path.isfile('crypto_data.csv'):
        df.to_csv('crypto_data.csv', index=False)
    else:
        df.to_csv('crypto_data.csv', mode='a', header=False, index=False)

def reset_monthly_counter():
    global calls_made
    calls_made = 0

# Infinite loop to keep the script running
while True:
    current_time = datetime.datetime.now()

    # Reset the counter at the beginning of a new month
    if current_time.day == 1 and current_time.hour == 0 and current_time.minute == 0:
        reset_monthly_counter()

    # Check if we have reached the monthly limit
    if calls_made < MONTHLY_LIMIT:
        api_runner()
        print('API Runner completed')
        calls_made += 1
        sleep(240)  # Sleep for 240 seconds (4 minutes)
    else:
        # Calculate seconds until the start of the next month to sleep
        next_month = (current_time.replace(day=28) + datetime.timedelta(days=4)).replace(day=1, hour=0, minute=0, second=0, microsecond=0)
        seconds_until_next_month = (next_month - current_time).total_seconds()
        print(f'Monthly limit reached. Sleeping for {seconds_until_next_month} seconds.')
        sleep(seconds_until_next_month + 1)  # Sleep until the start of the next month
```
