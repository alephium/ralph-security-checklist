# AlphPad Contract Security Assessment

In April 2024, AlphPad engaged Alephium core devs to assess the security of their contracts. This evaluation took approximately two person-days to complete.

The assessment was structured as follows:

- Gain a high-level understanding of the project and review the corresponding implementation.
- Review the core contracts in accordance with the best practices of the Alephium tech stack.

Overall, we found that the codebase adheres to best practices, maintaining a high level of quality. No major concerns were identified during our assessment. Our feedback primarily focused on enhancing the code and ensuring alignment with the Alephium stack.

The AlphPad team has promptly addressed all necessary improvements based on our feedback.
- Initial commit hash for review: `745a386`
- Final commit hash: `0a94b37`

Below, you'll find a summary of the checks performed on the contracts. A checkmark indicates that we have checked a specific item.

## Common
- [x] Are events used for proper logging?
- [x] Are user-friendly error codes provided?
- [x] Is the return value from low-level calls checked?
- [x] Testing
  * High test coverage
  * Unit tests covering all critical edge cases
  * Extensive integration tests
  * Code Freeze
- [x] Use a contract to receive protocol fees instead of address to avoid too many UTXOs generated

## Public Functions
- [x] Should it be public ?
- [x] Does the function need to check caller ? If so, is it checked properly
- [x] Does the function use assets properly ?
- [x] Are the inputs checked ?
- [x] Can edge case inputs (0, max) result in an unexpected behavior ?
- [x] Is the code comments coherent with the implementation ?

## Maths

- [x] Token amounts are dealt with the right units
- [x] Is the calculation even correct ?
- [x] Is there precision lost ? (especially for year/month/day calculation)
- [x] Always * before /
- [x] When < or > check if it should not be ≤ or ≥

## Control access

- [x] Centralization risk: `Admin key for contract upgrade is implemented with timelocks, following best practices.`
  * Executors can perform token transfers on behalf of user ?
  * Reclaiming / withdrawing any tokens ?
  * Total upgradeability ?
  * Instant parameters change (no timelock) ?
  * Can pause freely ?
  * Can rug user and steal assets ?
  * Bugs that lead restricted function to steal all the assets is a centralization risk
- [x] Can corrupted owner destroy the protocol ?
- [x] Is a features lacking access controls ?
- [x] Are timelocks used for important operations so that the users have time to observe upcoming changes ?
- [x] Are critical functions accessible ?

## Merkle trees
- [x] Are leafs hashed with the claimable address inside?
- [x] What happen if we pass the zero hash?
- [x] What happen if the exact same proof exist twice in the tree?

## General tips
- [x] For logic implemented several times, see if there are any differences and then standardize the logic.
- [x] Timelocks should be implemented for every protocol upgrade/change. (to let users exit if they don’t agree)
- [x] Beware of Oracle manipulation: Don't use spot price from an AMM as an oracle.
- [x] When pause mechanism :
  * can pause something that should not be pause (e.g liquidation)
  * Check can brick the contract
  * Check if whenNotPaused is well implemented on every functions where it needs to be
