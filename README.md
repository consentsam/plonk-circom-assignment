# PLONK Circom Assignment

The goal of this assignment is to make you familiar with the tooling that snarkjs and circom provide for verification of proof.

In this assignment, we have provided a simple [circuit](circuits/evaluation.circom), [input](input.json) and a [trusted setup](ptau/pot12_final.ptau).

To complete this assignment, you need to verify which proof from the proofs [directory](proofs/) is valid for the given circuit and expected output (input signal `expected_op` in the circuit) - `2649978643504`.

## Evaluation

- Clone this repo

    ```
    git clone CLONE_URL
    ```

- Create a new branch. You can use the following command

    ```
    git checkout -b BRANCH_NAME
    ```

- Once you determine the valid proof from the `proofs/` directory, move it to `valid_proofs/` directory

- Place your verification key file - `verification_key.json` (it should be named the same) you have used in the base directory

- Create a pull request from your branch to the main branch of the repo

- This assignment's evaluation is automated. Successful completion of the github action means your solution is correct. You can also check the status of the assignment's completion on the portal

## Resources

1. [PLONK Circom Walkthrough](https://github.com/ZKCamp/plonk-circom-walkthrough-public)
