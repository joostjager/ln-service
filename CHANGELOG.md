# Versions

## 43.2.0

- `getNode` added `is_omitting_channels`. This is recommended if not getting channels.

## 43.1.0

- `subscribeToTransactions` include the derived output addresses in chain_transaction event

## 43.0.0

- `getForwardingReputations` add support for general peer reputations

### Breaking Changes

- `getForwardingReputations` returns either channel or peer odds depending on lnd version

## 42.0.2

- Fix `closeChannel` to allow specifying a channel id when closing a channel
- Add `connectWatchtower` to connect to a watchtower
- Add `disconnectWatchtower` to disconnect a watchtower
- Add `getConnectedWatchtowers` to get watchtowers and watchtower info
- Add `isDestinationPayable` to check if a destination is payable
- Add `probeForRoute` option `is_ignoring_past_failures` to ignore mission control in probe
- Add `updateConnectedWatchtower`  to update a connected watchtower

### Breaking Changes

- `getRoutes`: `timeout` argument for the final cltv delta is renamed `cltv_delta`
- `getRoutes`: `fee` argument for the max fee is renamed `max_fee`
- `pay` max timeout rename: `timeout_height` to `max_timeout_height`
- `payViaPaymentDetails`: max cltv rename: `timeout_height` to `max_timeout_height`
- `payViaPaymentRequest`: max cltv rename: `timeout_height` to `max_timeout_height`
- `probeForRoute`: Ignoring below probability option `ignore_probability_below` eliminated
- `subscribeToPayViaDetails`: max cltv rename: `timeout_height` to `max_timeout_height`
- `subscribeToProbe`: max cltv rename: `timeout_height` to `max_timeout_height`
- `subscribeToProbe`: remove `ignore_probability_below`

## 41.3.0

- Add hop hints strictness option to getRoutes to only find routes that go through specified routes
- Add hop hints strictness to subscribeToProbe, probeForRoute

## 41.2.0

- Add outgoing channel support to getRoutes
- Pad the final CLTV of getRoutes output
- Add is_synced_to_graph to getWalletInfo

## 41.1.4

- Add watchtower server status method
- Improve compatibility with lnd 0.7.1

## 41.0.1

- Abstract out accounting methods to [ln-accounting](https://github.com/alexbosworth/ln-accounting)
- Standardize the output of `verify_message` to match expectations

## 40.4.4

- Add support for route hints in payment details
- Add support for failure reasons in router rpc payments
- Add support for reserve tokens in get channels

## 40.3.0

- Allow using mission control probabilities in probing

## 40.2.0

- Add support for getting chain receives in accounting report

## 40.1.3

- Add support for deleting all payments

## 40.0.1

- Avoid returning null transaction ids in graph updates

## 39.2.2

- Add uris to getWalletInfo method

## 39.1.1

- Add getPaymentOdds method to calculate the odds of a successful payment

Fixes:

- Add missing subscribeToPayViaRequest

## 39.0.0

All previously cbk type functions can now also be used as Promises

- Add deleteForwardingReputations to clear mission control reputations
- Add getForwardingReputations to get mission control reputations
- Add getPayment method to lookup a payment
- Add payViaPaymentDetails method to make a payment using deconstructed details
- Add payViaPaymentRequest method to make a payment using BOLT 11 pay request
- Add subscribeToPastPayment to subscribe to a payment's status
- Add subscribeToPayViaDetails to make a payment using details and sub to it
- Add subscribeToPayViaRequest to make a payment using a request and sub to it

### Breaking Changes

- All promisified methods are removed
- Response type strings are being phased out
- Open channel static fee amount is no longer subtracted
- Open channel requires an explicit local amount
- `subscribeToBackup` emits named events
- `subscribeToBlocks` emits named events
- `subscribeToChannels` emits named events
- `subscribeToGraph` emits named events
- `subscribeToInvoice` emits named events
- `subscribeToInvoices` emits named events

## 38.3.9

- Add helper method for probing to find a route
- Emit a payment in flight event for pay via routes subscription

## 38.2.0

- Add support for returning original payment request in getPayments

## 38.1.0

- Add support for paying via routes in the routerrpc API.
- Add support for node color in getWalletInfo
- Add support for watching arbitrary output scripts when subscribing to address
- Add support for returning chain ids in getWalletInfo

## 38.0.0

### Breaking Changes

`lightningDaemon` is renamed to `authenticatedLndGrpc` and
`unauthenticatedLndGrpc` and there is no more need to pass a service argument.

These two methods also now return their result wrapped in `lnd` in an object.
Pass the object wrapped in `lnd` to methods and they will now select the
appropriate service automatically.

`pay` arguments have been renamed:

- `max_fee` replaces `fee`
- `outgoing_channel` replaces `out`
- `timeout_height` replaces `timeout`

`pay` also has a new argument for use when specifying a path:
`pathfinding_timeout`. This is the cutoff time for starting a new pay attempt.

There have been multiple error codes changed
