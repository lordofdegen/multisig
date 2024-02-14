# Multisig

An example of a multisig to execute arbitrary Solana transactions.

This program can be used to allow a multisig to govern anything a regular
Pubkey can govern. One can use the multisig as a BPF program upgrade
authority, a mint authority, etc.

To use, one must first create a `Multisig` account, specifying two important
parameters:

1. Owners - the set of addresses that sign transactions for the multisig.
2. Threshold - the number of signers required to execute a transaction.

Once the `Multisig` account is created, one can create a `Transaction`
account, specifying the parameters for a normal Solana transaction.

To sign, owners should invoke the `approve` instruction, and finally,
the `execute_transaction`, once enough (i.e. `threshold`) of the owners have
signed.

## Note

* **This code (0.9.0) is [audited](./SECURITY_AUDIT_REPORT.pdf). Audit commissioned by [Streamflow](https://github.com/streamflow-finance).**

## Developing

[Anchor](https://github.com/coral-xyz/anchor) is used for developoment, and it's
recommended workflow is used here. To get started, see the [guide](https://anchor-lang.com).

### Build

```bash
anchor build --verifiable
```

The `--verifiable` flag should be used before deploying so that your build artifacts
can be deterministically generated with docker.

### Test

```bash
anchor test
```

### Verify

To verify the program deployed on Solana matches your local source code, install
docker, `cd programs/multisig`, and run

```bash
anchor verify <program-id | write-buffer>
```

A list of build artifacts can be found under [releases](https://github.com/coral-xyz/multisig/releases).
