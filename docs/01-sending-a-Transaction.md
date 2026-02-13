# What happen when you send a Bitcoin Transaction

## 1. The intent: sending value, not interacting with a system

At the human level, a Bitcoin transaction starts with a simple intent:

*Adi wants to send 0.01 BTC to Bittu.
*

This intent is deceptively simple.
Bitcoin does not understand balances, users, or accounts.
It only understands valid state transitions.

Everything that follows is the system’s attempt to answer one question:

*“Is this proposed change to the ledger valid according to the rules?”
*
There is no central service you submit a transaction to.
There is no guarantee that intent will be accepted.
There is only a proposal, and a network that independently evaluates it.

## 2. What a wallet really is (and what it is not)

A Bitcoin wallet does not store Bitcoin.

A wallet stores:

    1. cryptographic private keys

    2. the ability to discover unspent outputs associated with those keys

    3. logic to construct and sign transactions~~

Bitcoin itself exists only as unspent transaction outputs (UTXOs) recorded in the global ledger.

**UTXOs, not balances**

Instead of balances, Bitcoin tracks UTXOs.

A UTXO represents:

    1. a specific amount of bitcoin

    2. locked by a condition (usually a public key hash)

    3. created by a previous transaction

    4. not yet spent

When Adi’s wallet shows “1 BTC”, what it really means is:

*“There exist one or more UTXOs, spendable by Adi’s keys, whose total value is 1 BTC.”
*
This distinction matters because Bitcoin transactions consume and create UTXOs.
They do not modify balances.

## 3. Constructing the transaction: proposing a new state

To send 0.01 BTC, Alice’s wallet must construct a transaction that satisfies Bitcoin’s rules.

At a high level, a Bitcoin transaction contains:

    1. inputs: references to existing UTXOs being spent

    2. outputs: new UTXOs being created

    3. signatures: proofs that the spender is authorized

**Inputs: proving the right to spend**

Each input points to:

    a. a previous transaction

    b. a specific output index in that transaction

By referencing a UTXO, Adi is saying:

*“I want to consume this output and replace it with new ones.”
*
The wallet must then provide a valid signature that satisfies the spending condition of that UTXO.

Importantly:

    1. Inputs must exist

    2. Inputs must be unspent

    3. Inputs must be validly authorized

If any of these fail, the transaction is invalid.

**Outputs: specifying where value goes**

The transaction creates new outputs:

    1. one output sending 0.01 BTC to Bob

    2. usually one change output sending the remaining value back to Adi

Bitcoin does not automatically calculate change.
If Adi spends a 0.5 BTC UTXO to send 0.01 BTC, the remaining 0.49 BTC must be explicitly assigned — otherwise it becomes a transaction fee.

This is why most transactions have:

    1. one “payment” output

    2. one “change” output

**Signatures: authorization, not identity**

Signatures in Bitcoin do not prove identity.
They prove control over a key.

By signing the transaction, Adi demonstrates:

    1. she controls the private keys required to spend the referenced UTXOs

    2. she agrees to the exact inputs and outputs specified

Any modification to the transaction invalidates the signature.

At this point, the transaction is fully constructed — but nothing has happened yet.

No bitcoin has moved.
No ledger has changed.
The transaction is merely a proposal.

Next:
    *How this proposal is broadcast to the network,
    how nodes decide whether to accept or reject it,
    and why “sending” does not mean “confirmed”.*