# CHANGELOG

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.27.0] - 2022-01-10

### Added

- @arkonjs/tendermint-rpc: Add `hash` field to `BroadcastTxAsyncResponse`
  ([#938]).
- @arkonjs/stargate: Add `denomMetadata` and `denomsMetadata` to `BankExtension`
  ([#932]).
- @arkonjs/stargate: Merge `DeliverTxFailure` and `DeliverTxSuccess` into a
  single `DeliverTxResponse` ([#878], [#949]). Add `assertIsDeliverTxFailure`.
- @arkonjs/stargate: Created initial `MintExtension`.
- @arkonjs/stargate: Created `types.Dec` decoder function
  `decodeCosmosSdkDecFromProto`.
- @arkonjs/amino: Added `StdTx`, `isStdTx` and `makeStdTx` and removed them from
  @arkonjs/launchpad. They are re-exported in @arkonjs/launchpad for backwards
  compatibility.
- @arkonjs/stargate: Add `GasPrice.toString`.

[#938]: https://github.com/NLGRF/arkonjs/issues/938
[#932]: https://github.com/NLGRF/arkonjs/issues/932
[#878]: https://github.com/NLGRF/arkonjs/issues/878
[#949]: https://github.com/NLGRF/arkonjs/issues/949

### Fixed

- @arkonjs/tendermint-rpc: Add missing `BlockSearchResponse` case to `Response`.

### Changed

- @arkonjs/stargate: Remove verified queries from `AuthExtension` and
  `BankExtension` as well as `StargateClient.getAccountVerified` because the
  storage layout is not stable across multiple Cosmos SDK releases. Verified
  queries remain available in the `IbcExtension` because for IBC the storage
  layout is standardized. Such queries can still be implemented in CosmJS caller
  code that only needs to support one backend. ([#865])
- @arkonjs/tendermint-rpc: Remove default URL from `HttpClient` and
  `WebsocketClient` constructors ([#897]).
- all: Upgrade cosmjs-types to 0.4. This includes the types of the Cosmos SDK
  0.44 modules x/authz and x/feegrant. It causes a few breaking changes by
  adding fields to interfaces as well as changing `Date` to a `Timestamp`
  object. ([#928])
- @arkonjs/stargate and @arkonjs/cosmwasm-stargate: Add simulation support
  ([#931]).
- @arkonjs/tendermint-rpc: Remove `Tendermint33Client` and related symbols.
- @arkonjs/cosmwasm-stargate: Add support for wasmd 0.21. This changes the AMINO
  JSON representation of `Msg{Execute,Instantiate,Migrate}Contract.msg` from
  base64 strings to JSON objects. ([#948])
- @arkonjs/cli: Replace `colors` dependency with `chalk` (see
  https://snyk.io/blog/open-source-npm-packages-colors-faker/)

[#865]: https://github.com/NLGRF/arkonjs/issues/865
[#897]: https://github.com/NLGRF/arkonjs/issues/897
[#928]: https://github.com/NLGRF/arkonjs/issues/928
[#931]: https://github.com/NLGRF/arkonjs/pull/931
[#709]: https://github.com/NLGRF/arkonjs/issues/709
[#948]: https://github.com/NLGRF/arkonjs/pull/948

## [0.26.6] - 2022-01-10

### Changed

- @arkonjs/cli: Replace `colors` dependency with `chalk` (see
  https://snyk.io/blog/open-source-npm-packages-colors-faker/)

## [0.26.5] - 2021-11-20

### Added

- @arkonjs/amino: The `coin` and `coins` helpers now support both `number` and
  `string` as input types for the amount. This is useful if your values exceed
  the safe integer range.

### Fixed

- @arkonjs/tendermint-rpc: Fix undefined `this` in `decodeBroadcastTxAsync` and
  `broadcastTxAsync` ([#937]).

[#937]: https://github.com/NLGRF/arkonjs/pull/937

## [0.26.4] - 2021-10-28

### Fixed

- @arkonjs/cosmwasm-stargate: Fix response error handling for smart queries.

## [0.26.3] - 2021-10-25

### Added

- @arkonjs/ledger-amino: Add support for using forks of the Cosmos Ledger app by
  adding the fields `LaunchpadLedgerOptions.ledgerAppName` and
  `.minLedgerAppVersion`.

### Deprecated

- @arkonjs/stargate: The verified queries from `AuthExtension` and
  `BankExtension` as well as `StargateClient.getAccountVerified` are deprecated
  and will be removed in 0.27 ([#910]).

[#910]: https://github.com/NLGRF/arkonjs/pull/910

## [0.26.2] - 2021-10-12

### Fixed

- @arkonjs/stargate: remove extra space in messageTimeout registry.
- @arkonjs/cosmwasm-stargate: Fix Amino JSON representation of
  `MsgInstantiateContract`, `MsgMigrateContract` and `MsgExecuteContract` to
  match the wasmd expectation. This was broken since the wasmd upgrade to
  Stargate such that no Ledger signing was possible for those message types in
  the meantime.

## [0.26.1] - 2021-09-30

### Added

- @arkonjs/amino: `decodeBech32Pubkey` and `decodeAminoPubkey` now support
  decoding multisig public keys ([#882]).

### Fixed

- @arkonjs/stargate: Add missing pagination key arguments to query types in
  `GovExtension`.

[#882]: https://github.com/NLGRF/arkonjs/issues/882

## [0.26.0] - 2021-08-24

### Added

- @arkonjs/tendermint-rpc: `Tendermint34Client.blockSearch` and
  `Tendermint34Client.blockSearchAll` were added to allow searching blocks in
  Tendermint 0.34.9+ backends.
- @arkonjs/tendermint-rpc: `Tendermint33Client` has been added to provide support
  for Tendermint v0.33.
- @arkonjs/tendermint-rpc: Exports relating to `Tendermint33Client` are now
  available under `tendermint33`.
- @arkonjs/proto-signing and @arkonjs/stargate: Create a Stargate-ready
  `parseCoins` that replaces the `parseCoins` re-export from `@arkonjs/amino`.
- @arkonjs/cosmwasm-stargate: Export `isValidBuilder`, which is a clone of
  `isValidBuilder` from @arkonjs/cosmwasm-launchpad.
- @arkonjs/cosmwasm-stargate: Copy symbols `Code`, `CodeDetails`, `Contract`,
  `ContractCodeHistoryEntry` and `JsonObject` from @arkonjs/cosmwasm-launchpad
  and remove dependency on @arkonjs/cosmwasm-launchpad.
- @arkonjs/faucet: Add new configuration variable `FAUCET_PATH_PATTERN` to
  configure the HD path of the faucet accounts ([#832]).
- @arkonjs/cosmwasm-stargate: Add field `ibcPortId` to `Contract` ([#836]).
- @arkonjs/stargate: Add `GovExtension` for query client.
- @arkonjs/stargate: Add support for `MsgDeposit`, `MsgSubmitProposal` and
  `MsgVote`.

[#832]: https://github.com/NLGRF/arkonjs/issues/832
[#836]: https://github.com/NLGRF/arkonjs/issues/836

### Changed

- @arkonjs/cosmwasm-launchpad: The `transferAmount` property on
  `InstantiateOptions` (accepted as a parameter to
  `SigningCosmWasmClient.instantiate`) has been renamed to `funds`.
- @arkonjs/cosmwasm-stargate: The `transferAmount` property on
  `InstantiateOptions` (accepted as a parameter to
  `SigningCosmWasmClient.instantiate`) has been renamed to `funds`.
- @arkonjs/cosmwasm-stargate: Default fee/gas values have been removed. Fees now
  need to be calculated and passed to `SigningCosmWasmClient` when calling any
  methods which submit transactions to the blockchain.
- @arkonjs/stargate: Default fee/gas values have been removed. Fees now need to
  be calculated and passed to `SigningStargateClient` when calling any methods
  which submit transactions to the blockchain.
- @arkonjs/tendermint-rpc: Make `tendermint34.Header.lastBlockId` and
  `tendermint34.Block.lastCommit` optional to better handle the case of height 1
  where there is no previous block.
- @arkonjs/proto-signing: `makeAuthInfoBytes` now takes an array of pubkey
  sequence pairs in order to support different sequences for different signers.
- @arkonjs/cosmwasm-stargate: Upgraded client to support wasmd 0.18 backends.
  Other backends are not supported anymore. Update proto types from
  `cosmwasm.wasm.v1beta1.*` to `cosmwasm.wasm.v1.*`. `MsgStoreCode.source` and
  `MsgStoreCode.builder` were removed; `MsgInstantiateContract.initMsg` and
  `MsgMigrateContract.migrateMsg` were renamed to `msg`; `Code.{source,builder}`
  and `CodeDetails.{source,builder}` were removed; `isValidBuilder` was removed;
  `UploadMeta` and the `meta` from `SigningCosmWasmClient.upload` were removed.
  ([#863])

[#863]: https://github.com/NLGRF/arkonjs/pull/863

### Removed

- Node.js v10 is no longer supported. Please use v12 or later.
- @arkonjs/cosmwasm-stargate: Remove `CosmWasmFeeTable` type and
  `defaultGasLimits` object.
- @arkonjs/stargate: Remove types, objects and functions to do with default fees:
  `CosmosFeeTable`, `FeeTable`, `GasLimits`, `defaultGasLimits`,
  `defaultGasPrice` and `buildFeeTable`.
- @arkonjs/tendermint-rpc: `Client` has been removed. Please use
  `Tendermint33Client` or `Tendermint34Client`, depending on your needs.
- @arkonjs/cosmwasm: Package removed ([#786]).
- @arkonjs/cosmwasm-launchpad: Package removed ([#786]).

[#786]: https://github.com/NLGRF/arkonjs/issues/786

### Fixed

- @arkonjs/socket: Upgrade dependency "ws" to version 7 to avoid potential
  security problems.

## [0.25.6] - 2021-07-26

### Fixed

- @arkonjs/stargate: Fix types `AminoMsgTransfer` and `AminoHeight` as well as
  the encoding of `MsgTransfer` for Amino signing.

## [0.25.5] - 2021-06-23

### Added

- @arkonjs/tendermint-rpc: `Tendermint34Client.blockSearch` and
  `Tendermint34Client.blockSearchAll` were added to allow searching blocks in
  Tendermint 0.34.9+ backends. This is a backport of [#815]. Note: Decoding
  blocks of height 1 is unsupported. This is fixed in [#815] and will be
  released as part of CosmJS 0.26.

[#815]: https://github.com/NLGRF/arkonjs/pull/815

## [0.25.4] - 2021-05-31

### Fixed

- @arkonjs/socket: Upgrade dependency "ws" to version 7 to avoid potential
  security problems.

## [0.25.3] - 2021-05-18

### Fixed

- @arkonjs/cosmwasm-stargate, @arkonjs/stargate: Fix error propagation in
  `CosmWasmClient.broadcastTx` and `StargateClient.broadcastTx` ([#800]). This
  bug was introduced with the switch from broadcast mode "commit" to "sync" in
  version 0.25.0.
- @arkonjs/launchpad, @arkonjs/stargate: Avoid the use of named capture groups in
  `GasPrice.fromString` to restore ES2017 compatibility and make the library
  work with Hermes ([#801]; thanks [@AlexBHarley]).
- @arkonjs/launchpad: Adapt `GasPrice.fromString` denom pattern to Cosmos SDK
  0.39 rules: reduce denom length to 16 and allow digits in denom.
- @arkonjs/stargate: Adapt `GasPrice.fromString` denom pattern to Cosmos SDK 0.42
  rules: allow lengths up to 128, allow upper case letters and digits.

[#800]: https://github.com/NLGRF/arkonjs/issues/800
[#801]: https://github.com/NLGRF/arkonjs/issues/801
[@alexbharley]: https://github.com/AlexBHarley

## [0.25.2] - 2021-05-11

### Added

- @arkonjs/cosmwasm-stargate: Add `broadcastTimeoutMs` and
  `broadcastPollIntervalMs` options added to `SigningCosmWasmClientOptions`.
- @arkonjs/proto-signing: Add `serialize` and `serializeWithEncryptionKey`
  methods to `DirectSecp256k1HdWallet`. Also add `deserialize` and
  `deserializeWithEncryptionKey` static methods.
- @arkonjs/proto-signing: Export `extractKdfConfiguration` and `executeKdf`
  helper functions and `KdfConfiguration` type.
- @arkonjs/proto-signing: Export `makeCosmoshubPath` helper.
- @arkonjs/stargate: Export `makeCosmoshubPath` helper.
- @arkonjs/stargate: Add `broadcastTimeoutMs` and `broadcastPollIntervalMs`
  options added to `SigningStargateClientOptions`.

## [0.25.1] - 2021-05-06

### Added

- @arkonjs/cosmwasm-stargate: Export types `Code`, `CodeDetails`, `Contract`,
  `ContractCodeHistoryEntry` and `JsonObject` which are response types of
  `CosmWasmClient` methods. Export types `ChangeAdminResult`, `ExecuteResult`,
  `InstantiateOptions`, `InstantiateResult`, `MigrateResult`, `UploadMeta` and
  `UploadResult` which are argument or response types of `SigningCosmWasmClient`
  methods.

### Fixed

- @arkonjs/cosmwasm-stargate: Use `CosmWasmFeeTable` instead of `CosmosFeeTable`
  in `SigningCosmWasmClientOptions`; export type `CosmWasmFeeTable`.
- @arkonjs/amino, @arkonjs/cli, @arkonjs/ledger-amino, @arkonjs/proto-signing: Fix
  runtime error caused by passing explicitly undefined options.

## [0.25.0] - 2021-05-05

### Added

- @arkonjs/cosmwasm-launchpad: Expose `SigningCosmWasmClient.fees`.
- @arkonjs/cosmwasm-stargate: Expose `SigningCosmWasmClient.fees` and
  `SigningCosmWasmClient.registry`.
- @arkonjs/launchpad: Expose `SigningCosmosClient.fees`.
- @arkonjs/stargate: Expose `SigningStargateClient.fees` and
  `SigningStargateClient.registry`.
- @arkonjs/stargate: Add support for different account types in `accountFromAny`
  and `StargateClient`. Added `ModuleAccount` and vesting accounts
  `BaseVestingAccount`, `ContinuousVestingAccount`, `DelayedVestingAccount` and
  `PeriodicVestingAccount`.
- @arkonjs/stargate: Add codecs for IBC channel tx, client query/tx, and
  connection tx, as well as Tendermint.
- @arkonjs/stargate: Add support for IBC message types in
  `SigningStargateClient`.
- @arkonjs/stargate: Added new `logs` export with all the functionality from
  @arkonjs/launchpad.
- @arkonjs/stargate: Added new `Coin`, `coin`, `coins` and `parseCoins` exports
  which have the same functionality as already existed in @arkonjs/launchpad.
- @arkonjs/amino: New package created that contains the shared amino signing
  functionality for @arkonjs/launchpad and @arkonjs/stargate.
- @arkonjs/amino: Split public key interfaces into `Pubkey`, `SinglePubkey` and
  `Secp256k1Pubkey` where `Pubkey` is a generalization of the old `PubKey` that
  supported nested pubkeys for multisig. `SinglePubkey` is the old `PubKey` in
  which the `value` is a base64 encoded string. And `Secp256k1Pubkey` is a
  single secp256k1 pubkey.
- @arkonjs/utils: The new `arrayContentStartsWith` works similar to
  `arrayContentEquals` but only checks the start of an array.
- @arkonjs/proto-signing: Added new `Coin`, `coin`, `coins` and `parseCoins`
  exports which have the same functionality as already existed in
  @arkonjs/launchpad.
- @arkonjs/stargate: Add `SigningStargateClient.sign`, which allows you to create
  signed transactions without broadcasting them directly. The new type
  `SignerData` can be passed into `.sign` to skip querying account number,
  sequence and chain ID
- @arkonjs/cosmwasm-stargate: Add `SigningCosmWasmClient.sign`, which allows you
  to create signed transactions without broadcasting them directly. The new type
  `SignerData` from @arkonjs/stargate can be passed into `.sign` to skip querying
  account number, sequence and chain ID.
- @arkonjs/stargate: Add constructor `SigningStargateClient.offline` which does
  not connect to Tendermint. This allows offline signing.
- @arkonjs/stargate: Add `makeMultisignedTx` which allows you to assemble a
  transaction signed by a multisig account.
- @arkonjs/stargate: Add `delegateTokens`, `undelegateTokens` and
  `withdrawRewards` methods to `SigningStargateClient`.
- @arkonjs/stargate: Export `defaultGasLimits` and `defaultGasPrice`.
- @arkonjs/cosmwasm-stargate: Export `defaultGasLimits`.
- @arkonjs/stargate: `SigningStargateClient` constructor is now `protected`.
- @arkonjs/cosmwasm-stargate: `SigningCosmWasmClient` constructor is now
  `protected`.
- @arkonjs/cosmwasm-stargate: Add `SigningCosmWasmClient.offline` static method
  for constructing offline clients without a Tendermint client.
- @arkonjs/stargate: Add `SigningStargateClient.sendIbcTokens` method.
- @arkonjs/amino: Export `Secp256k1HdWalletOptions` interface.
- @arkonjs/amino: Add `bip39Password` option to `Secp256k1HdWallet` options.
- @arkonjs/proto-signing: Export `DirectSecp256k1HdWalletOptions` interface.
- @arkonjs/proto-signing: Add `bip39Password` option to `DirectSecp256k1HdWallet`
  options.
- @arkonjs/amino: Add `rawEd25519PubkeyToRawAddress` helper function.
- @arkonjs/tendermint-rpc: Add `pubkeyToAddress`, `pubkeyToRawAddress`,
  `rawEd25519PubkeyToRawAddress`, and `rawSecp256k1PubkeyToRawAddress` helper
  functions.
- @arkonjs/stargate: `StargateClient.broadcastTx` and `.getTx` results now
  include `gasUsed` and `gasWanted` properties.
- @arkonjs/cosmwasm-stargate: `CosmWasmClient.broadcastTx` and `.getTx` results
  now include `gasUsed` and `gasWanted` properties.
- @arkonjs/proto-signing: Export `DecodeObject` and `TxBodyEncodeObject`
  interfaces as well as `isTxBodyEncodeObject` helper function.
- @arkonjs/stargate: Add `MsgDelegateEncodeObject`, `MsgSendEncodeObject`,
  `MsgTransferEncodeObject`, `MsgUndelegateEncodeObject` and
  `MsgWithdrawDelegatorRewardEncodeObject` interfaces as well as
  `isMsgDelegateEncodeObject` etc helpers.
- @arkonjs/cosmwasm-stargate: Add `MsgClearAdminEncodeObject`,
  `MsgExecuteContractEncodeObject`, `MsgInstantiateContractEncodeObject`,
  `MsgMigrateContractEncodeObject`, `MsgStoreCodeEncodeObject` and
  `MsgUpdateAdminEncodeObject` interfaces as well as
  `isMsgClearAdminEncodeObject` etc helpers.
- @arkonjs/stargate: Add transfer queries codec, as well as transfer query
  methods to IBC query extension.
- @arkonjs/tendermint-rpc: Export `ValidatorSecp256k1Pubkey` interface.
- @arkonjs/proto-signing: Add transaction decoder `decodeTxRaw` for decoding
  transaction bytes returned by Tendermint (e.g. in `IndexedTx.tx`).

### Changed

- @arkonjs/cosmwasm-stargate: Codec adapted to support wasmd 0.16. Older versions
  of wasmd are not supported anymore.
- @arkonjs/stargate: Let `AuthExtension.account` and
  `AuthExtension.unverified.account` return an account of type `Any`. This makes
  the caller responsible for decoding the type.
- @arkonjs/stargate: Remove `accountFromProto` in favour of `accountFromAny`.
- @arkonjs/stargate: Rename `Rpc` interface to `ProtobufRpcClient` and
  `createRpc` to `createProtobufRpcClient`.
- @arkonjs/stargate: Reorganize nesting structure of IBC query client and add
  support for more methods.
- @arkonjs/tendermint-rpc: The fields `CommitSignature.validatorAddress`,
  `.timestamp` and `.signature` are now optional. They are unset when
  `blockIdFlag` is `BlockIdFlag.Absent`. The decoding into `CommitSignature` is
  only updated for the class `Tendermint34Client`, not for `Client`. Please
  migrate to the former.
- @arkonjs/launchpad: `rawSecp256k1PubkeyToAddress` was removed. Instead use
  `Bech32.encode(prefix, rawSecp256k1PubkeyToRawAddress(pubkeyRaw))` with
  `rawSecp256k1PubkeyToRawAddress` from @arkonjs/amino.
- @arkonjs/stargate: `parseRawLog` is now nested under the `logs` export.
- @arkonjs/stargate: Query extensions now have unverified queries at the root and
  verified queries nested under `.verified`.
- @arkonjs/cosmwasm-stargate: `wasm` extension now has unverified queries at the
  root.
- @arkonjs/stargate: `StargateClient.getAccount` now uses an unverified query and
  `StargateClient.getAccountUnverified` has been removed.
  `StargateClient.getAccountVerified` has been added, which performs a verified
  query.
- @arkonjs/cosmwasm-stargate: `CosmWasmClient.getAccount` now uses an unverified
  query and `CosmWasmClient.getAccountUnverified` has been removed.
  `CosmWasmClient.getAccountVerified` has been added, which performs a verified
  query.
- @arkonjs/stargate: `StargateClient.getSequence` now rejects if the account is
  not found, instead of returning null.
- @arkonjs/stargate: `StargateClient.getBalance` now returns a 0 balance instead
  of null.
- @arkonjs/stargate: `StargateClient.getAllBalancesUnverified` has been renamed
  `.getAllBalances`.
- @arkonjs/cosmwasm-stargate: `CosmWasmClient.getSequence` now rejects if the
  account is not found, instead of returning null.
- @arkonjs/cosmwasm-stargate: `CosmWasmClient.getBalance` now returns a 0 balance
  instead of null.
- @arkonjs/amino: Options for `Secp256k1HdWallet.fromMnemonic` are now passed via
  a `Secp256k1HdWalletOptions` object.
- @arkonjs/proto-signing: Options for `DirectSecp256k1HdWallet.fromMnemonic` are
  now passed via a `DirectSecp256k1HdWalletOptions` object.
- @arkonjs/stargate: `StargateClient.broadcastTx` now uses sync mode and then
  polls for the transaction before resolving. The timeout and poll interval can
  be configured.
- @arkonjs/cosmwasm-stargate: `CosmWasmClient.broadcastTx` now uses sync mode and
  then polls for the transaction before resolving. The timeout and poll interval
  can be configured.
- @arkonjs/tendermint-rpc: Tendermint v34 `TxData` type now includes `codeSpace`,
  `gasWanted`, and `gasUsed` properties.
- @arkonjs/amino: `Secp256k1HdWallet.fromMnemonic` now accepts a
  `Secp256k1HdWalletOptions` argument which includes an array of `hdPaths`
  instead of a single `hdPath`. `Secp256k1HdWallet.generate` now also accepts
  options via this interface. This adds support for multiple accounts from the
  same mnemonic to `Secp256k1HdWallet`.
- @arkonjs/proto-signing: `DirectSecp256k1HdWallet.fromMnemonic` now accepts a
  `DirectSecp256k1HdWalletOptions` argument which includes an array of `hdPaths`
  instead of a single `hdPath`. `DirectSecp256k1HdWallet.generate` now also
  accepts options via this interface. This adds support for multiple accounts
  from the same mnemonic to `DirectSecp256k1HdWallet`.
- @arkonjs/tendermint-rpc: `ValidatorPubkey` is now a union of
  `ValidatorEd25519Pubkey` and the newly exported `ValidatorSecp256k1Pubkey`
  interface.
- @arkonjs/tendermint-rpc: `decodePubkey` now supports secp256k1 public keys.

### Deprecated

- @arkonjs/tendermint-rpc: `Client` has been deprecated. Launchpad applications
  do not need a Tendermint RPC client and Stargate applications should use
  `Tendermint34Client`.

### Removed

- @arkonjs/stargate: `coinFromProto` helper has been removed as it is no longer
  needed after the `ts-proto` migration.

## [0.24.1] - 2021-03-12

CHANGELOG entries missing. Please see [the diff][0.24.1].

## [0.24.0] - 2021-03-11

- @arkonjs/cosmwasm: This package is now deprecated. The same functionality is
  now available in @arkonjs/cosmwasm-launchpad.
- @arkonjs/cosmwasm: `logs` is no longer exported. Use `logs` from
  @arkonjs/launchpad instead.
- @arkonjs/cosmwasm: Export `JsonObject`, `ChangeAdminResult` and `WasmData`
  types as well as `isValidBuilder` and `parseWasmData` functions.
- @arkonjs/cosmwasm: Add `CosmWasmClient.getTx` method for searching by ID and
  remove such functionality from `CosmWasmClient.searchTx`.
- @arkonjs/cosmwasm: Rename `SigningCosmWasmClient.senderAddress` to
  `.signerAddress`.
- @arkonjs/cosmwasm-stargate: Add new package for CosmWasm Stargate support.
- @arkonjs/crypto: Change `Secp256k1Keypair` from tagged type to simple
  interface.
- @arkonjs/launchpad: Add `Secp256k1Wallet` to manage a single raw secp256k1
  keypair.
- @arkonjs/launchpad: `OfflineSigner` type’s `sign` method renamed `signAmino`
  and `SignResponse` type renamed `AminoSignResponse`.
- @arkonjs/launchpad: `Secp256k1HdWallet.sign` method renamed `signAmino`.
- @arkonjs/launchpad: Add `CosmosClient.getTx` method for searching by ID and
  remove such functionality from `CosmosClient.searchTx`.
- @arkonjs/launchpad: Add `SigningCosmosClient.sign` method for signing without
  broadcasting.
- @arkonjs/launchpad: Add `SigningCosmosClient.appendSignature` method creating
  transactions with multiple signatures.
- @arkonjs/launchpad: Add support for undefined memo in `makeSignDoc`.
- @arkonjs/launchpad: Rename `SigningCosmosClient.senderAddress` to
  `.signerAddress`.
- @arkonjs/proto-signing: Add new package for handling transaction signing with
  protobuf encoding.
- @arkonjs/proto-signing: Expose `DirectSignResponse` interface.
- @arkonjs/stargate: Add new package for Cosmos SDK Stargate support.
- @arkonjs/tendermint-rpc: Make `Client.detectVersion` private and let it return
  a version instead of a client.
- @arkonjs/tendermint-rpc: Make the constructor of `Client` private. Add
  `Client.create` for creating a Tendermint client given an RPC client and an
  optional adaptor.
- @arkonjs/tendermint-rpc: Add an optional adaptor argument to `Client.connect`
  which allows skipping the auto-detection.
- @arkonjs/tendermint-rpc: Remove export `v0_33` in favour of `adaptor33` and
  `adaptor34`. Export the `Adaptor` type.
- @arkonjs/tendermint-rpc: Export `DateTime` class.
- @arkonjs/tendermint-rpc: Remove types `QueryString`, `Base64String`,
  `HexString`, `IntegerString` and `IpPortString`. Use `string` instead.
- @arkonjs/tendermint-rpc: Remove types `BlockHash`, `TxBytes` and `TxHash`. Use
  `Uint8Array` instead.

### Added

- @arkonjs/launchpad: Export distribution module msg types
  `MsgFundCommunityPool`, `MsgSetWithdrawAddress`, `MsgWithdrawDelegatorReward`,
  `MsgWithdrawValidatorCommission` and type checker helper functions.
- @arkonjs/utils: Added `assertDefinedAndNotNull`.
- @arkonjs/tendermint-rpc: The new `Tendermint34Client` is a copy of the old
  `Client` but without the automatic version detection. Its usage is encouraged
  over `Client` if you connect to a Tendermint 0.34 backend.

### Changed

- @arkonjs/encoding: Change return type of `fromRfc3339` from `ReadonlyDate` to
  `Date` as the caller becomes the owner of the object and can safely mutate it
  in any way.
- @arkonjs/launchpad-ledger: Renamed to @arkonjs/ledger-amino.
- @arkonjs/ledger-amino: `LedgerSigner.sign` method renamed `signAmino`.

### Deprecated

- @arkonjs/tendermint-rpc: Deprecate `DateTime` in favour of the free functions
  `fromRfc3339WithNanoseconds` and `toRfc3339WithNanoseconds`.

## 0.23.2 (2021-01-06)

### Security

- @arkonjs/cli: Update vulnerable axios dependency.
- @arkonjs/faucet-client: Update vulnerable axios dependency.
- @arkonjs/launchpad: Update vulnerable axios dependency.
- @arkonjs/tendermint-rpc: Update vulnerable axios dependency.

## 0.23.1 (2020-10-27)

- @arkonjs/crypto: Export new convenience functions `keccak256`, `ripemd160`,
  `sha1`, `sha256` and `sha512`.
- @arkonjs/faucet-client: Add new package which exports `FaucetClient` class.

## 0.23.0 (2020-10-09)

- @arkonjs/cli: Expose `HdPath` type.
- @arkonjs/cosmwasm: Rename `CosmWasmClient.postTx` method to `.broadcastTx`.
- @arkonjs/cosmwasm: Rename `FeeTable` type to `CosmWasmFeeTable`.
- @arkonjs/cosmwasm: `SigningCosmWasmClient` constructor now takes optional
  arguments `gasPrice` and `gasLimits` instead of `customFees` for easier
  customization.
- @arkonjs/cosmwasm: Rename `SigningCosmWasmClient.signAndPost` method to
  `.signAndBroadcast`.
- @arkonjs/cosmwasm: Use stricter type `Record<string, unknown>` for smart query,
  init, migrate and handle messages (in `WasmExtension.wasm.queryContractSmart`,
  `CosmWasmClient.queryContractSmart`, `SigningCosmWasmClient.instantiate`,
  `SigningCosmWasmClient.migrate`, `SigningCosmWasmClient.execute`).
- @arkonjs/crypto: Export new type alias `HdPath`.
- @arkonjs/crypto: Add `Secp256k1Signature.toFixedLength` method.
- @arkonjs/demo-staking: Remove package and supporting scripts.
- @arkonjs/encoding: Add `limit` parameter to `Bech32.encode` and `.decode`. The
  new default limit for decoding is infinity (was 90 before). Set it to 90 to
  create a strict decoder.
- @arkonjs/faucet: Environmental variable `FAUCET_FEE` renamed to
  `FAUCET_GAS_PRICE` and now only accepts one token. Environmental variable
  `FAUCET_GAS` renamed to `FAUCET_GAS_LIMIT`.
- @arkonjs/faucet: `/credit` API now expects `denom` (base token) instead of
  `ticker` (unit token). Environmental variables specifying credit amounts now
  need to use uppercase denom.
- @arkonjs/launchpad: Rename `FeeTable` type to `CosmosFeeTable` and export a new
  more generic type `FeeTable`.
- @arkonjs/launchpad: Add new class `GasPrice`, new helper type `GasLimits` and
  new helper function `buildFeeTable` for easier handling of gas prices and
  fees.
- @arkonjs/launchpad: Rename `CosmosClient.postTx` method to `.broadcastTx`.
- @arkonjs/launchpad: `SigningCosmosClient` constructor now takes optional
  arguments `gasPrice` and `gasLimits` instead of `customFees` for easier
  customization.
- @arkonjs/launchpad: Rename `SigningCosmosClient.signAndPost` method to
  `.signAndBroadcast`.
- @arkonjs/launchpad: Rename `PostTx`-related types to `BroadcastTxResult`,
  `BroadcastTxSuccess` and `BroadcastTxFailure` respectively, as well as helper
  functions `isBroadcastTxFailure`, `isBroadcastTxSuccess` and
  `assertIsBroadcastTxSuccess`.
- @arkonjs/launchpad: Export `isSearchByIdQuery`, `isSearchByHeightQuery`,
  `isSearchBySentFromOrToQuery` and `isSearchByTagsQuery`.
- @arkonjs/launchpad: Change type of `TxsResponse.logs` and
  `BroadcastTxsResponse.logs` to `unknown[]`.
- @arkonjs/launchpad: Export `StdSignDoc` and create helpers to make and
  serialize a `StdSignDoc`: `makeSignDoc` and `serializeSignDoc`.
- @arkonjs/launchpad: Let `OfflineSigner.sign` take an `StdSignDoc` instead of an
  encoded message and return a `SignResponse` that includes the document which
  was signed.
- @arkonjs/launchpad: Remove `PrehashType` and the prehash type argument in
  `OfflineSigner.sign` because the signer now needs to know how to serialize an
  `StdSignDoc`.
- @arkonjs/launchpad: Remove `makeSignBytes` in favour of `makeSignDoc` and
  `serializeSignDoc`.
- @arkonjs/launchpad: Create `WrappedTx`, `WrappedStdTx` and `isWrappedStdTx` to
  better represent the Amino tx interface. Deprecate `CosmosSdkTx`, which is an
  alias for `WrappedStdTx`.
- @arkonjs/launchpad: Add `makeStdTx` to create an `StdTx`.
- @arkonjs/launchpad: Rename `Secp256k1Wallet` to `Secp256k1HdWallet`. Later on,
  we'll use `Secp256k1Wallet` for single key wallets.
- @arkonjs/launchpad-ledger: Add package supporting Ledger device integration for
  Launchpad. Two new classes are provided: `LedgerSigner` (for most use cases)
  and `LaunchpadLedger` for more fine-grained access.
- @arkonjs/math: Add `.multiply` method to `Decimal` class.
- @arkonjs/math: Deprecate `Uint32.fromBigEndianBytes` in favour of
  `Uint32.fromBytes`, which supports both big and little endian.
- @arkonjs/math: Deprecate `Uint64.fromBytesBigEndian` in favour of
  `Uint64.fromBytes`, which supports both big and little endian.
- @arkonjs/math: Add `Uint32.fromString`.
- @arkonjs/tendermint-rpc: Make `BroadcastTxCommitResponse.height` non-optional.
- @arkonjs/tendermint-rpc: Make `TxProof.proof.leafHash` non-optional because it
  is always set.
- @arkonjs/tendermint-rpc: Change type of `GenesisResponse.appState` to
  `Record<string, unknown> | undefined`.
- @arkonjs/tendermint-rpc: Remove obsolete `TxData.tags` and make `TxData.events`
  non-optional. Rename `Tag` to `Attribute`.
- @arkonjs/tendermint-rpc: Remove obsolete `BlockResultsResponse.beginBlock` and
  `.beginBlock`. The new `.beginBlockEvents` and `.endBlockEvents` now parse the
  events correctly.
- @arkonjs/tendermint-rpc: Remove trivial helpers `getTxEventHeight`,
  `getHeaderEventHeight` and `getBlockEventHeight` because they don't do
  anything else than accessing an object member.
- @arkonjs/tendermint-rpc: Add support for connecting to Tendermint RPC 0.34.
- @arkonjs/tendermint-rpc: Make `TxEvent.index` optional and deprecate it because
  it is not set anymore in Tendermint 0.34.
- @arkonjs/utils: Add `assertDefined`.
- @arkonjs/faucet: Rename binary from `cosmwasm-faucet` to `cosmos-faucet`.

## 0.22.3 (2020-09-15)

- @arkonjs/math: Add `Decimal.minus`.

## 0.22.2 (2020-08-11)

- @arkonjs/faucet: Log errors for failed send transactions.
- @arkonjs/faucet: Add config variable `FAUCET_MEMO`.
- @arkonjs/faucet: Add config variables `FAUCET_FEE` and `FAUCET_GAS`.
- @arkonjs/launchpad: Add `parseCoins` helper.

## 0.22.1 (2020-08-11)

- @arkonjs/cli: Import `encodeAminoPubkey`, `encodeBech32Pubkey`,
  `decodeAminoPubkey` and `decodeBech32Pubkey` by default.
- @arkonjs/launchpad: Add ed25519 support to `encodeBech32Pubkey`.
- @arkonjs/launchpad: Add `encodeAminoPubkey` and `decodeAminoPubkey`.
- @arkonjs/utils: Add `arrayContentEquals`.
- @arkonjs/faucet: Add config variables `FAUCET_ADDRESS_PREFIX` and
  `FAUCET_TOKENS`.
- @arkonjs/faucet: Remove broken chain ID from `cosmwasm-faucet generate`.

## 0.22.0 (2020-08-03)

- @arkonjs/cli: Now supports HTTPs URLs for `--init` code sources.
- @arkonjs/cli: Now supports adding code directly via `--code`.
- @arkonjs/cosmwasm: Rename `CosmWasmClient.getNonce` method to `.getSequence`.
- @arkonjs/cosmwasm: Remove `RestClient` class in favour of new modular
  `LcdClient` class from @arkonjs/sdk38.
- @arkonjs/cosmwasm: Add `SigningCosmWasmClient.signAndPost` as a mid-level
  abstraction between `SigningCosmWasmClient.upload`/`.instantiate`/`.execute`
  and `.postTx`.
- @arkonjs/cosmwasm: Use `*PostTx*` types and helpers from @arkonjs/sdk38. Remove
  exported `PostTxResult`.
- @arkonjs/cosmwasm: `ContractDetails` was removed in favour of just `Contract`.
  The missing `init_msg` is now available via the contract's code history (see
  `getContractCodeHistory`).
- @arkonjs/cosmwasm: Remove `SigningCallback` in favour of the `OfflineSigner`
  interface.
- @arkonjs/sdk38: Rename `CosmosClient.getNonce` method to `.getSequence`.
- @arkonjs/sdk38: Remove `RestClient` class in favour of new modular `LcdClient`
  class.
- @arkonjs/sdk38: Remove `Pen` type in favour of `OfflineSigner` and remove
  `Secp256k1Pen` class in favour of `Secp256k1Wallet` which takes an
  `OfflineSigner` instead of a `SigningCallback`.
- @arkonjs/sdk38: Rename `CosmosSdkAccount` to `BaseAccount` and export the type.
- @arkonjs/sdk38: `BaseAccount` now uses `number | string` as the type for
  `account_number` and `sequence`. The new helpers `uint64ToNumber` and
  `uint64ToString` allow you to normalize the mixed input.
- @arkonjs/sdk38: `BaseAccount` now uses `string | PubKey | null` as the type for
  `public_key`. The new helper `normalizePubkey` allows you to normalize the
  mixed input.
- @arkonjs/math: Add missing integer check to `Uint64.fromNumber`. Before
  `Uint64.fromNumber(1.1)` produced some result.
- @arkonjs/sdk38: Add `SigningCosmosClient.signAndPost` as a mid-level
  abstraction between `SigningCosmosClient.sendTokens` and `.postTx`.
- @arkonjs/sdk38: Export `PostTxFailure`/`PostTxSuccess` and type checkers
  `isPostTxFailure`/`isPostTxSuccess`; export `assertIsPostTxSuccess`.
- @arkonjs/sdk38: `Secp256k1Wallet`s can now be generated randomly with
  `Secp256k1Wallet.generate(n)` where `n` is 12, 15, 18, 21 or 24 mnemonic
  words.
- @arkonjs/sdk38: The new `Secp256k1Wallet.serialize` and `.deserialize` allow
  encrypted serialization of the wallet.
- @arkonjs/sdk38: Remove the obsolete `upload`, `init`, `exec` properties from
  `FeeTable`. @arkonjs/cosmwasm has its own `FeeTable` with those properties.
- @arkonjs/sdk38: Rename package to @arkonjs/launchpad.

[unreleased]: https://github.com/NLGRF/arkonjs/compare/v0.27.0...HEAD
[0.27.0]: https://github.com/NLGRF/arkonjs/compare/v0.26.6...v0.27.0
[0.26.6]: https://github.com/NLGRF/arkonjs/compare/v0.26.5...v0.26.6
[0.26.5]: https://github.com/NLGRF/arkonjs/compare/v0.26.4...v0.26.5
[0.26.4]: https://github.com/NLGRF/arkonjs/compare/v0.26.3...v0.26.4
[0.26.3]: https://github.com/NLGRF/arkonjs/compare/v0.26.2...v0.26.3
[0.26.2]: https://github.com/NLGRF/arkonjs/compare/v0.26.1...v0.26.2
[0.26.1]: https://github.com/NLGRF/arkonjs/compare/v0.26.0...v0.26.1
[0.26.0]: https://github.com/NLGRF/arkonjs/compare/v0.25.6...v0.26.0
[0.25.6]: https://github.com/NLGRF/arkonjs/compare/v0.25.5...v0.25.6
[0.25.5]: https://github.com/NLGRF/arkonjs/compare/v0.25.4...v0.25.5
[0.25.4]: https://github.com/NLGRF/arkonjs/compare/v0.25.3...v0.25.4
[0.25.3]: https://github.com/NLGRF/arkonjs/compare/v0.25.2...v0.25.3
[0.25.2]: https://github.com/NLGRF/arkonjs/compare/v0.25.1...v0.25.2
[0.25.1]: https://github.com/NLGRF/arkonjs/compare/v0.25.0...v0.25.1
[0.25.0]: https://github.com/NLGRF/arkonjs/compare/v0.24.1...v0.25.0
[0.24.1]: https://github.com/NLGRF/arkonjs/compare/v0.24.0...v0.24.1
[0.24.0]: https://github.com/NLGRF/arkonjs/compare/v0.23.0...v0.24.0
