# Ralph security checklist

## Common
- [ ] Are events used for proper logging?
- [ ] Are user-friendly error codes provided?
- [ ] Is the return value from low-level calls checked?
- [ ] Who has control over privileged accounts, and what are the mechanisms for control?
- [ ] Is there a single private key controlling the contract, or is a multisig setup used?

## Public Functions
- [ ] Should it be public ?
- [ ] Does the function need to check caller ? If so, is it checked properly
- [ ] Does the function use assets properly ?
- [ ] Are the inputs checked ?
- [ ] Can edge case inputs (0, max) result of an unexpected behavior ?
- [ ] Is the code comments coherent with the implementation ?

## Maths

- [ ] Is the calculation even correct ?
- [ ] Is there precision lost ? (especially for year/month/day calculation)
- [ ] Always * before /
- [ ] When < or > check if it should not be ≤ or ≥

## Control access

- [ ] Centralization risk
  * Executors can perform token transfers on behalf of user ?
  * Reclaiming / withdrawing any tokens ?
  * Total upgradeability ?
  * Instant parameters change (no timelock) ?
  * Can pause freely ?
  * Can rug user and steal assets ?
  * Bugs that lead restricted function to steal all the assets is a centralization risk
- [ ] Can corrupted owner destroy the protocol ?
- [ ] Is a features lacking access controls ?
- [ ] Is the owner change a two step process ?
- [ ] Are critical functions accesible ?

## Signatures
- [ ] Are signatures protected against replay with a nonce and block.chainid ?
- [ ] Is the Signature used from the right person ?

## Merkle trees
- [ ] Are leafs hashed with the claimable address inside?
- [ ] What happen if we pass the zero hash?
- [ ] What happen if the exact same proof exist twice in the tree?

## General tips
- [ ] For logic implemented several times, see if there are any differences and then standardize the logic.
- [ ] Timelocks should be implemented for every protocol upgrade/change. (to let users exit if they don’t agree)
- [ ] Beware of Oracle manipulation: Don't use spot price from an AMM as an oracle.
- [ ] When pause mechanism :
  * can pause something that should not be pause (e.g liquidation)
  * Check can brick the contract
  * Check if whenNotPaused is well implemented on every functions where it needs to be
