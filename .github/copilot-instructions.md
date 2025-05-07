# GitHub Copilot Instructions for Aiken Smart Contracts

This file outlines specific guidelines for GitHub Copilot to optimize its assistance in developing, testing, and reviewing Aiken smart contracts.

## Objectives for Copilot
- Enable developers to write secure, readable, and efficient Aiken smart contracts.
- Suggest best practices, patterns, and idiomatic Aiken code.
- Assist in debugging and testing Aiken smart contracts.
- Provide meaningful comments and context for generated code.

## Key Instructions for Copilot

### General Guidance
1. **Security First**:
   - Prioritize secure coding practices in all suggestions.
   - Propose input validation and error handling where applicable.
2. **Adhere to Standards**:
   - Follow the patterns and principles outlined in `.github/BEST_PRACTICES.md`.
   - Use modular and reusable code structures.
3. **Code Quality**:
   - Ensure readability through clean formatting and meaningful variable names.
   - Include inline comments for complex or abstract logic.

### Aiken-Specific Instructions
1. **Leverage the Standard Library**:
   - Prioritize using functions from Aiken's standard library when available.
   - Reference appropriate modules from `aiken-lang/stdlib` repository.
2. **Type System Usage**:
   - Utilize Aiken's strong type system for safer code.
   - Suggest custom types for domain-specific concepts.
3. **Testing Patterns**:
   - Recommend comprehensive test cases with the built-in test framework.
   - Suggest property-based testing with the fuzz library where appropriate.
4. **Validator Structure**:
   - Follow idiomatic structure for validator scripts.
   - Use appropriate datum, redeemer, and context patterns.
5. **Plutus Compatibility**:
   - Be mindful of the compilation to Plutus Core.
   - Suggest optimizations that consider the underlying execution model.

### Plutus V3 Contract Development
1. **Production Contract References**:
   - Reference real-world patterns from successful Plutus V3 projects like SundaeSwap V3, Minswap V2, and JPG Store.
   - Provide guidance based on patterns in `.github/PLUTUS_V3_PATTERNS.md`.
2. **Cardano-Specific Features**:
   - Use reference inputs for accessing immutable data without consuming UTxOs.
   - Utilize reference scripts for reusing validator scripts and reducing transaction size.
   - Implement inline datums when appropriate for transaction outputs.
3. **Performance Optimization**:
   - Suggest data structure optimizations for on-chain storage.
   - Recommend script size reduction techniques to stay within limits.
   - Provide memory usage patterns that reduce execution costs.
4. **Advanced Patterns**:
   - Provide guidance on implementing state machines and multi-stage validations.
   - Suggest patterns for contract composability and interoperability.
   - Offer solutions for common Cardano-specific challenges like UTxO management.

## Example Use Cases
Here are some prompts developers may use with Copilot:
- "Write a smart contract for a token system in Aiken."
- "Generate test cases for a staking contract."
- "Optimize this Aiken contract for performance."
- "Create a validator that checks for specific NFT ownership."
- "Implement a multi-signature scheme in Aiken."
- "Write a property-based test for this validation logic."
- "Create a DEX-style swap contract with Plutus V3 features."
- "Implement a validator that uses reference inputs for oracle data."
- "Design a contract that follows the Minswap V2 pattern for batch processing."

## Aiken Ecosystem Integration
When working with the broader Aiken ecosystem:
1. **Editor Integration**:
   - Suggest appropriate VSCode settings for the Aiken extension.
   - Help configure editor-specific features for Aiken development.
2. **GitHub Actions**:
   - Provide workflows for CI/CD with Aiken's GitHub Actions.
   - Suggest test and documentation generation steps.
3. **Project Structure**:
   - Follow the conventional Aiken project structure.
   - Organize code into appropriate modules and packages.

## Production-Ready Contract Development
1. **Reference Production Implementations**:
   - Suggest patterns based on battle-tested contracts in the ecosystem.
   - Reference implementations from the [awesome-aiken](https://github.com/aiken-lang/awesome-aiken) repository.
2. **Performance Considerations**:
   - Provide guidance on execution cost optimization.
   - Suggest memory-efficient data structures for on-chain use.
3. **Deployment Readiness**:
   - Assist with preparing contracts for mainnet deployment.
   - Recommend testing strategies before production use.

## Feedback and Improvement
Developers are encouraged to:
- Review Copilot's suggestions carefully.
- Refine and adapt the code to meet specific project needs.
- Provide feedback to improve Copilot's understanding over time.

## Resource References
- Include relevant files and examples from:
  - `contracts/` directory for Aiken contract implementations.
  - `tests/` directory for test cases.
  - `.github/BEST_PRACTICES.md` for security and efficiency guidelines.
  - `.github/PLUTUS_V3_PATTERNS.md` for production-grade Plutus V3 patterns.
  - [Aiken Documentation](https://aiken-lang.org/) for official guidance.
  - [Awesome Aiken](https://github.com/aiken-lang/awesome-aiken) for community resources.