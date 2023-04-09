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


## Followed Commands

- Since we have been provided with a `.ptau` file, we don't need to generate one and hence we will start from step 4 of [PLONK Circom Walkthrough](https://github.com/ZKCamp/plonk-circom-walkthrough-public) and so run the following command
    ```
    circom circuits/evaluation.circom --r1cs --wasm --sym
    ```
- Once you have generated the `r1cs` and  `wasm` files, you should move to the next step i.e. generating witness file by running the following command
    ```
    node evaluation_js/generate_witness.js evaluation_js/evaluation.wasm input.json witness.wtns
    ```

- After generating the witness, you should try to generate a `.zkey` file by running the following command
    ```
    snarkjs plonk setup evaluation.r1cs ptau/pot12_final.ptau evaluation.zkey
    ```

- Now we will export this verification key into JSON format as follows:
    ```
    snarkjs zkey export verificationkey evaluation.zkey verification_key.json
    ```

- Now generate zk proof and json containing public values for verifier
    ```
    snarkjs plonk prove evaluation.zkey witness.wtns proof.json public.json
    ```

- Now that you have generated your proof, you can run the following command to make sure that you are getting this message in your console `[INFO]  snarkJS: OK!`. If you are getting this message, that means your proof is valid.
    ```
    snarkjs plonk verify verification_key.json public.json proof.json
    ```

- Since we have to find the valid proof among the provided proofs in the directory `proofs`, I would just run the command in the previous step and see for which of the proof files,I would get the message `[INFO]  snarkJS: OK!`

- The following messages got printed for the proofs in the folder

    | Proof Files | Console Message                                |
    |-------------|------------------------------------------------|
    | proof1.json | [ERROR] snarkJS: Proof is not well constructed |
    | proof2.json | [ERROR] snarkJS: Proof is not well constructed |
    | proof3.json | [ERROR] snarkJS: Proof is not well constructed |
    | proof4.json | [INFO]  snarkJS: OK! |
    | proof5.json | [ERROR] snarkJS: Proof is not well constructed |

- As can be seen in the above logs, proof4.json is valid and hence I would copy the file into the folder `valid_proof` by running the command
    ```
    cp proofs/proof4.json valid_proofs 
    ```

- Now, close the editor and go to sleep 😛


## Resources

1. [PLONK Circom Walkthrough](https://github.com/ZKCamp/plonk-circom-walkthrough-public)


