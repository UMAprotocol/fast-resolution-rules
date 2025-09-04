# Fast Resolution Rules

This repository hosts rules for resolving fast resolution assertions on UMA enhancing the `ASSERT_TRUTH` price identifier used. The claim being evaluated must be formatted as stringified JSON object including at least following key-value pairs:
- `valueAsserted`: numerical value to be evaluated.
- `requestIdentifier`: string identifier that must match any of below specified supported request identifiers. These include links to more specific instructions on how a particular asserted value should be evaluated:
  - [BINANCE_CANDLE_UP_DOWN](./polymarket/binance-candle-up-down.md)
- `requestData`: stringified JSON object that should be used as additional context for evaluating the asserted value based on the instructions for the provided `requestIdentifier`.
- `assertionTimestamp`: UNIX epoch timestamp in seconds at which a given assertion should be evaluated. This must not be larger than the block timestamp when the asserted claim was emitted in the corresponding `AssertionMade` event.

If some of above required information is missing or has invalid value the asserted claim should be evaluated as `false`.

As an illustration, the claim relying on fast assertion rules could be formatted as `{"title":"Binance candle is Up or Down","valueAsserted":0,"options":{"0":"DOWN","1":"UP"},"requestIdentifier":"BINANCE_CANDLE_UP_DOWN","requestKey":"0x575926346221801313287f612d3ad6def86f00eb5f00fc89751e292fa3be0bf8","requestData":{"symbol":"BTCUSDT","startTime":1699995600000,"endTime":1699999199999,"interval":"1h"},"assertionTimestamp":1700000000,"rulesLink":"https://github.com/UMAprotocol/fast-resolution-rules/"}`

