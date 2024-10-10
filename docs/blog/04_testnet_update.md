# Announcing Testnet

<!-- TODO change this date -->
Published on: 2024-10-XX

Today, a community of operators launches the first public Walrus Testnet.
This is an important milestone in validating the operation of Walrus as a decentralized blob store,
by operating it on a set of independent storage nodes, that change over time through a delegated
proof of stake mechanism. The Testnet also brings functionality updates relating to governance,
epochs, and blob deletion.

## Blob deletion

The most important user-facing new feature is optional blob deletion. The uploader of a blob can
optionally indicate a blob is "deletable". This information is stored in the Sui blob meta-data
object, and is also included in the event denoting when the blob is certified. Subsequently, the
owner of the Sui blob meta-data object can "delete" it. As a result storage for the remaining
period is reclaimed and can be used by subsequent blob storage operations.

Blob deletion allows more fine grained storage cost management: smart contracts that wrap blob
meta-data objects can define logic that stores blobs and delete them to minimize costs, and reclaim
storage space before Walrus epochs end.

However, blob deletion is not an effective privacy mechanism in itself: copies of the blob may exist
outside Walrus storage nodes on caches and end-user stores
or devices. Furthermore, if the identical blob is stored by multiple Walrus users, the blob will
still be available on Walrus until no copy exists. Thus deleting your own copy of a blob cannot
guarantee that it is deleted from Walrus as a whole.

- Find out how to
  [upload and delete deletable blobs](../usage/client-cli.md#reclaiming-space-via-deletable-blobs)
  thought the CLI.
- Find out more about how [delete operations work](../dev-guide/dev-operations.md#delete).

## Epochs

Walrus Testnet enables multiple epochs. Initially an epoch is a single day to ensure the logic of
epoch change is thoroughly tested. At Mainnet epochs will likely be multiple weeks long.

Now stored blob expiry epoch is meaningful, and blobs will become unavailable after their expiry
epoch. The store command may be used to extend the expiry epoch of a blob that is still available.
This operation is efficient and only affects payments and meta-data, and does not re-upload blob
contents.

- Find out the [current epoch](../usage/client-cli.md#walrus-system-information) through the CLI.
- Find out how to store a blob for
  [multiple epochs](../usage/client-cli.md#storing-querying-status-and-reading-blobs).

## The WAL token and the Testnet WAL faucet

Payments for blob storage and extending blob expiry are denominated in Testnet WAL, a
Walrus token issued on the Sui Testnet. Testnet WAL has no value, and an unlimited supply - so no
need to covet or hoard it - its just for testing purposes and only issued on Sui Testnet.

To make Testnet WAL available to all who want to experiment with the Walrus Testnet we provide a
utility and smart contract to convert Testnet SUI (which also has no value) into Testnet WAL using
a one-to-one exchange rate. This is chosen arbitrarily, and generally one should not read too much
into the actual WAL denominated costs of storage on Testnet. They have been chosen arbitrarily.

- Find out how to [request Test WAL tokens](../usage/setup.md#testnet-wal-faucet) through the CLI.

## Decentralization through staking & unstaking

The WAL token may also be used to stake with storage operators. Staked WAL can be unstaked and
re-staked with other operators or used to purchase storage.

Each epoch storage nodes are selected and allocated storage shards according to their delegated
stake. At the end of each epoch payments for storing blobs for the epoch are distributed to storage
nodes and those that delegate stake to them. Furthermore, important network parameters - such as
total available storage and storage price - are set by the selected storage operators each epoch
according to their stake weight.

A staking web dapps is provided to experiment with this functionality. Community members have also
created explorers that can be used to view storage nodes when considering who to stake with. Staking
ensures that the ultimate governance of Walrus, directly in terms of storage nodes, and indirectly
in terms of parameters and software they chose, rests with WAL Token holders.

Under the hood and over the next months we will be testing many aspects of epoch changes and
storage node committee changes: better shard allocation mechanisms upon changes or storage node
stake; efficient ways to sync state between storage nodes; as well as better ways for storage nodes
to follow Sui event streams.

- Explore the [Walrus staking dapp]()
- Look at recent activity on the [Walrus Explorer]()

## New Move Contracts & documentation

As part of the Testnet release of Walrus the documentation and Move Smart contracts have been
updated, and can be found at the [Walrus-docs repository](https://github.com/MystenLabs/walrus-docs)
and as a [Walrus Docs Site](https://docs.walrus.site/).