# Plutus V3 Contract Patterns and Examples

This document provides a curated collection of Plutus V3 contract patterns and examples using the Aiken language. These resources demonstrate industry best practices from production Cardano applications.

## DeFi Contracts

DeFi applications showcase some of the most sophisticated Plutus V3 smart contract patterns:

### Decentralized Exchanges (DEX)

- [SundaeSwap V3](https://github.com/SundaeSwap-finance/sundae-contracts-aiken) - Advanced DEX implementation with concentrated liquidity
  - Key patterns: Multi-pool management, price oracles, concentrated liquidity positions
  - Notable features: Fee optimization, slippage protection

- [Minswap V2](https://github.com/minswap/minswap-contracts-aiken) - Efficient DEX contract suite
  - Key patterns: Batch order processing, yield farming integrations
  - Notable features: Order book compression, gas optimization techniques

- [Minswap Stableswap](https://github.com/minswap/minswap-contracts-aiken/tree/main/stableswap) - Specialized AMM for stablecoins
  - Key patterns: Custom bonding curves, low-slippage swaps
  - Notable features: Virtual assets, peg maintenance mechanisms

### Lending and Borrowing

- [Lenfi](https://github.com/lenfiLabs/lenfi-smart-contracts) - Decentralized lending protocol
  - Key patterns: Collateral management, interest rate models
  - Notable features: Liquidation mechanisms, risk parameters

- [Levvy](https://github.com/levvyio/levvy-contracts) - NFT-based lending and borrowing
  - Key patterns: NFT collateralization, oracle price feeds
  - Notable features: Floor price computation, liquidation strategies

### Stablecoins

- [Mehen](https://github.com/MehenFinance/mehen-contracts) - Fiat-backed stablecoin
  - Key patterns: Multi-sig treasury, compliance mechanisms
  - Notable features: Burning and minting policies, audit trails

## Marketplace Contracts

NFT and digital asset marketplaces implement complex patterns:

- [JPG Store](https://github.com/jpg-store/jpg-core) - Leading NFT marketplace on Cardano
  - Key patterns: Listing/offer mechanisms, royalty enforcement
  - Notable features: CIP-68 reference tokens, batch operations

- [Nebula](https://github.com/thirstywolf/nebula-contracts) - NFT marketplace with advanced features
  - Key patterns: Auction mechanisms, bundled sales
  - Notable features: Time-locked listings, dynamic pricing

## Data Structure Libraries

Efficient on-chain data structures:

- [merkle-patricia-forestry](https://github.com/aiken-lang/merkle-patricia-forestry) - Modified Merkle Patricia Tries
  - Key patterns: Authenticated data structures, key-value mappings
  - Notable features: Space-efficient proofs, incremental verification

- [aiken-linked-list](https://github.com/anastasia-labs/aiken-linked-list) - On-chain distributed linked lists
  - Key patterns: UTxO-based node representation, pointer traversal
  - Notable features: Concurrency scaling, persistent storage patterns

- [aiken-trie](https://github.com/anastasia-labs/aiken-trie) - Distributed tries
  - Key patterns: Prefix-based lookups, shared validator access
  - Notable features: Efficient key-value storage, tree-based indices

## Governance Frameworks

- [unLearn](https://github.com/unlearnlabs/aiken) - Modular governance framework
  - Key patterns: Voting mechanisms, proposal lifecycle management
  - Notable features: Delegation, quadratic voting, timelock controls

## Smart Wallets

- [Seedelf](https://github.com/SeedElf/seedelf-contracts) - Cardano Stealth Wallet
  - Key patterns: Multi-signature schemes, key derivation
  - Notable features: Spending conditions, stealth address generation

## Code Examples

### Validator with Reference Scripts (Plutus V3)

```aiken
use aiken/transaction.{ScriptContext, InlineDatum, find_input}
use aiken/transaction/value.{Value}
use aiken/script.{ScriptPurpose, Validator, ScriptHash}

type Datum {
  owner: ByteArray,
  reference_validators: List<ScriptHash>,
}

type Redeemer {
  action: Action,
  auth_index: Int,
}

type Action {
  Withdraw
  Delegate
}

validator {
  fn spend(datum: Datum, redeemer: Redeemer, ctx: ScriptContext) -> Bool {
    let ScriptContext { transaction, purpose } = ctx
    let reference_script = datum.reference_validators |> list.at(redeemer.auth_index)?
    
    // Find reference input containing the specified validator
    let reference_input = 
      transaction.reference_inputs
      |> list.find(fn(input) {
        when input.output.reference_script is {
          None -> False
          Some(script) -> script.hash() == reference_script
        }
      })?
    
    // Execute validation logic based on action
    when redeemer.action is {
      Withdraw -> {
        // Withdrawal logic using reference script
        let is_signed = transaction.is_signed_by(datum.owner)
        is_signed
      }
      Delegate -> {
        // Delegation logic using reference script
        True
      }
    }
  }
}
```

### Efficient UTxO Management Pattern

```aiken
use aiken/transaction.{ScriptContext, Input, Output}
use aiken/transaction/value.{Value, from_asset}
use aiken/hash.{Blake2b_224}

type Datum {
  owner: ByteArray,
  state_counter: Int,
}

type Redeemer {
  action: Action,
}

type Action {
  UpdateState(Int)
  Withdraw(Value)
}

validator {
  fn manage_utxo(datum: Datum, redeemer: Redeemer, ctx: ScriptContext) -> Bool {
    let ScriptContext { transaction, purpose } = ctx
    let this_address = ctx.get_spending_validator_hash()?
    
    // Find own outputs and verify state continuity
    when redeemer.action is {
      UpdateState(new_counter) -> {
        let own_outputs =
          transaction.outputs
          |> list.filter(fn(output) {
            output.address.payment_credential == Credential.Script(this_address)
          })
          
        when list.find(own_outputs, fn(output) {
          when output.datum is {
            InlineDatum(d) -> {
              let new_datum: Datum = d
              // Verify state transition is valid
              new_datum.owner == datum.owner && 
              new_datum.state_counter == datum.state_counter + 1
            }
            _ -> False
          }
        }) is {
          Some(_) -> True
          None -> False
        }
      }
      Withdraw(value) -> {
        // Ensure only owner can withdraw
        transaction.is_signed_by(datum.owner)
      }
    }
  }
}
```

## Integration with Cardano Features

Plutus V3 contracts can leverage these Cardano-specific features:

1. **Reference Inputs**: Access immutable data without consuming UTxOs
2. **Reference Scripts**: Reuse validator scripts to reduce transaction size
3. **Inline Datums**: Embed datum values directly in transaction outputs
4. **Script Context Functions**: Utilize the enhanced script context API
5. **Memory Limit Increases**: Build more complex validation logic

## Testing Strategies for Plutus V3

Effective testing approaches for Plutus V3 contracts:

1. **Property-Based Testing**: Use [aiken-lang/fuzz](https://github.com/aiken-lang/fuzz) for generating random test cases
2. **Integration Testing**: Test contract interaction with [sidan-lab/vodka](https://github.com/sidan-lab/vodka)
3. **Security Testing**: Exploit intentionally vulnerable contracts with [Cardano Capture The Flag](https://github.com/cardano-foundation/cardano-ctf)

## Performance Optimization Techniques

- **Script Size Optimization**: Refactor common functions into libraries
- **On-Chain Storage**: Use space-efficient encodings and data structures
- **Execution Steps**: Profile and optimize execution cost using benchmarks