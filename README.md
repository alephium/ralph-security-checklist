# Ralph security checklist

## Final Checks
- [ ] Are all contract tests passing in CI?
- [ ] Have all security recommendations been implemented?
- [ ] Does the project use the latest dApp stack of Alephium

## Common
- [ ] Are events used for proper logging?
- [ ] Are user-friendly error codes provided?
- [ ] Is the return value from low-level calls checked?
- [ ] Testing
  * Is there high test coverage?
  * Are unit tests covering all critical edge cases?
  * Are there extensive integration tests?
  * Is there a code Freeze before deployment?
- [ ] Is a contract used to receive protocol fees instead of address to avoid generating too many UTXOs?

## Public Functions
- [ ] Are function visibility and mutability correctly specified?
- [ ] Does the function need to check caller? If so, is it checked properly?
- [ ] Does the function use assets properly?
- [ ] Are the inputs validated?
- [ ] Can edge case inputs (e.g. 0, max values) result in an unexpected behavior?
- [ ] Are the code comments coherent with the implementation?

## Language Specific
- [ ] All value types used as reference types by accident?

## Maths

- [ ] Are token amounts handled with the correct units?
- [ ] Is the calculation correct?
- [ ] Is there any precision lost? (especially for year/month/day calculation)
- [ ] Are * performed before /?
- [ ] Are comparison checked correctly (e.g., < vs. ≤, > vs. ≥)?

## Access Control

- [ ] Are centralization risks addressed with best practices?
  * Can executors perform token transfers on behalf of the user?
  * Can any token be reclaimed or withdrawn?
  * Is there total upgradeability?
  * Are there instant parameter changes (no timelock)?
  * Can the contract be paused freely?
  * Can the contract be rugged to steal user assets?
  * Do bugs in restricted functions pose a centralization risk?
- [ ] Can a corrupted owner destroy the protocol?
- [ ] Are any features lacking access controls?
- [ ] Are timelocks used for important operations, allowing users time to observe upcoming changes?
- [ ] Are critical functions accessible?

## DoS
- [ ] Does the contract store a limited number of tokens (current limit: 8 tokens)?
- [ ] Could the contract block operations if there are insufficient assets (e.g. staking rewards)?
- [ ] Are loops and recursive calls optimized to prevent exceeding gas limits?

## Signatures
- [ ] Are signatures protected against replay with a nonce and block.chainid?
- [ ] Is the Signature used from the correct person?

## Merkle trees
- [ ] Are leaf nodes hashed with the claimable address inside?
- [ ] Does it handle zero hash properly?
- [ ] Does it handle duplicated values properly?

## General tips
- [ ] For logic implemented multiple times, are there any differences, and is the logic standardized?
- [ ] Are timelocks implemented for every protocol upgrade/change to allow users to exit if they disagree?
- [ ] Beware of Oracle manipulation: Don't use spot price from an AMM as an oracle.
- [ ] For pause mechanism :
  * Can something critical be paused (e.g., liquidation)?
  * Can the contract be bricked by pausing?
  * Is `whenNotPaused` implemented correctly in every function where needed?
