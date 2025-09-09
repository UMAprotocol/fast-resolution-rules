# BINANCE_CANDLE_UP_DOWN

The `BINANCE_CANDLE_UP_DOWN` identifier is used to assert claims on whether a given Binance candle closing price was higher or lower than its opening price. The `requestData` included in the asserted claim must include following key-value pairs that correspond to [Kline/Candlestick data](https://developers.binance.com/docs/binance-spot-api-docs/rest-api/market-data-endpoints#klinecandlestick-data) request parameters:
- `symbol`: trading pair string, e.g. `BTCUSDT`.
- `startTime`: UNIX epoch timestamp in milliseconds.
- `endTime`: UNIX epoch timestamp in milliseconds.
- `interval`: supported candlestick interval value, e.g. `1h`.

If some of above required parameters are missing or has invalid value the asserted claim should be evaluated as `false`.

If assertion validation timestamp (`assertionTimestamp`) converted to milliseconds is less than `endTime` request parameter, the asserted claim should be evaluated as `false`.

Based on above request parameter values one should make API request to Binance candlestick endpoint: `https://api.binance.com/api/v3/klines?symbol=${symbol}&interval=${interval}&startTime=${startTime}&endTime=${endTime}`. This should return exactly one matching candlestick data element in the array, otherwise the asserted claim should be evaluated as `false`. If the matching candlestick was returned one should compare its close price (the 5th element) against its open price (the 2nd element). If the close price is higher or equal to the open price, the expected asserted value is `1`, otherwise it is `0`.

The asserted claim should be evaluated as `true` only if all required data is present and the `valueAsserted` matches the expected value based on the Binance candlestick data as described above. Otherwise the asserted claim should evaluate to `false`.
