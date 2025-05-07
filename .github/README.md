# GitHub Copilot Instructions for Aiken Smart Contracts

This repository contains guidance for optimizing GitHub Copilot's assistance when developing smart contracts using Aiken, a modern smart contract platform for Cardano.

## What is Aiken?

Aiken is a purely functional language designed specifically for developing smart contracts on the Cardano blockchain. It features:

- A small, expressive syntax that can be learned quickly
- Strong type system to catch errors at compile time
- Built-in testing framework with property-based testing support
- Modern tooling for a productive development experience

## Repository Contents

- `.github/copilot-instructions.md`: Guidelines for GitHub Copilot to assist with Aiken development
- `.github/BEST_PRACTICES.md`: Coding standards, security practices, and patterns for Aiken
- `.github/PLUTUS_V3_PATTERNS.md`: Production-grade Plutus V3 contract patterns and examples
- `contracts/`: Example smart contract implementations
- `tests/`: Example test cases for the smart contracts

## Plutus V3 Contract Patterns

The `.github/PLUTUS_V3_PATTERNS.md` file contains a curated collection of production-grade Plutus V3 contract patterns implemented with Aiken:

- DeFi contracts (DEXes, lending protocols, stablecoins)
- NFT marketplaces with advanced features
- Efficient on-chain data structures 
- Governance frameworks and smart wallets
- Code examples with Plutus V3-specific optimization techniques

These examples illustrate best practices from real-world Cardano applications and can help Copilot generate better smart contract suggestions.

## Aiken Ecosystem Resources

The Aiken ecosystem includes several key components:

- [Aiken Compiler](https://github.com/aiken-lang/aiken): The core compiler and development tools
- [Standard Library](https://github.com/aiken-lang/stdlib): Common utilities and functions
- [Prelude](https://github.com/aiken-lang/prelude): Default imports available in all Aiken code
- [Fuzzing Library](https://github.com/aiken-lang/fuzz): Tools for property-based testing
- [Editor Integrations](https://github.com/aiken-lang/vscode-aiken): Extensions for various editors
- [Awesome Aiken](https://github.com/aiken-lang/awesome-aiken): Curated list of libraries and resources

For a comprehensive list of production Aiken projects, libraries, and learning resources, see the [awesome-aiken](https://github.com/aiken-lang/awesome-aiken) repository.

## Getting Started

1. Review the `.github/copilot-instructions.md` file to understand how to guide Copilot
2. Familiarize yourself with Aiken's best practices in `.github/BEST_PRACTICES.md`
3. Study the Plutus V3 patterns in `.github/PLUTUS_V3_PATTERNS.md` for advanced techniques
4. Explore the example contracts in the `contracts/` directory
5. See how tests are structured in the `tests/` directory

## Contributing

Contributions to improve these Copilot instructions are welcome! Please feel free to submit pull requests with:

- Additional example contracts
- Enhanced best practices
- More specific Copilot instructions for different use cases
- Additional resources that could be helpful

## Additional Resources

- [Aiken Documentation](https://aiken-lang.org/)
- [Aiken GitHub Organization](https://github.com/aiken-lang)
- [TxPipe's Discord](https://discord.gg/JYpuX9sFE8) - Community discussion