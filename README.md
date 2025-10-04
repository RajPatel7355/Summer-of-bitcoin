# Bitcoin Protocol and Transaction Engineering

This project, developed as part of the Summer of Bitcoin '25 program, is a deep dive into the technical workings of the Bitcoin protocol. It involves direct interaction with a Bitcoin Core node to create, sign, and broadcast complex, custom transactions. The project also includes a simulation of the block mining process to demonstrate a fundamental understanding of Bitcoin's consensus mechanism.

---

## Key Features

### 1. Custom Transaction Broadcasting
* **Bitcoin Core RPC Interaction:** Implemented scripts to communicate with a Bitcoin Core node using Remote Procedure Calls (RPC). This includes managing wallets, getting blockchain information, and broadcasting raw transactions.
* **`OP_RETURN` Outputs:** Created and broadcasted transactions with custom `OP_RETURN` outputs, allowing for the embedding of arbitrary data onto the blockchain.

### 2. Advanced Multisignature (Multisig) Transaction Construction
* **2-of-2 P2SH-P2WSH:** Built a complete Pay-to-Script-Hash (P2SH) wrapped Pay-to-Witness-Script-Hash (P2WSH) transaction. This is a modern, SegWit-compatible multisig scheme.
* **End-to-End Creation:** The process includes:
    * Deriving public/private key pairs using ECDSA.
    * Constructing the 2-of-2 `redeemScript` and `witnessScript`.
    * Generating the P2SH address.
    * Crafting the transaction with the correct inputs and outputs.

### 3. Manual Transaction Signing and Witness Creation
* **Sighash Computation:** Performed manual sighash (Signature Hash) calculations to create the correct message digest that needs to be signed, ensuring all parts of the transaction are properly committed.
* **ECDSA Signature Generation:** Used cryptographic libraries to generate valid ECDSA signatures for the transaction inputs.
* **Witness Stack Assembly:** Constructed the final `witness` stack, correctly ordering the signatures and the witness script to ensure the transaction is accepted by the network according to SegWit rules.

### 4. Block Mining Simulation
* **Mempool Validation:** Implemented a process to fetch and validate transactions from the mempool.
* **Block Header Construction:** Built a valid block header, including the Merkle Root of the selected transactions, timestamp, and previous block hash.
* **Proof-of-Work:** Simulated the mining process by iteratively hashing the block header with a changing nonce until a hash was found that met the network's difficulty target (i.e., a hash with a certain number of leading zeros).

---

## Technical Concepts Covered
* **Bitcoin Core:** RPC communication, wallet management.
* **Transaction Structure:** Inputs, Outputs, `nLockTime`, `OP_RETURN`.
* **Scripting:** `redeemScript`, `witnessScript`, `OP_CHECKSIG`.
* **Address Types:** P2SH, P2WSH, Bech32.
* **Cryptography:** ECDSA for key generation and signing, SHA256, HASH160.
* **Signing Process:** Sighash flags (`SIGHASH_ALL`), DER encoding.
* **SegWit:** Witness stack, P2SH-P2WSH wrapping.
* **Mining:** Block headers, Merkle trees, nonce, difficulty target, Proof-of-Work.

---

## How to Run

### Prerequisites
* Python 3.8+
* A running Bitcoin Core node (regtest mode is recommended for testing).
* `python-bitcoinlib` or similar libraries.

### Setup
1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```
2.  **Install dependencies:**
    ```sh
    pip install -r requirements.txt
    ```
3.  **Configure Bitcoin Core:** Ensure your `bitcoin.conf` file is set up for RPC access in `regtest` mode.
    ```conf
    regtest=1
    rpcuser=youruser
    rpcpassword=yourpassword
    server=1
    txindex=1
    ```
4.  **Run the scripts:**
    Execute the Python scripts from the command line.
    ```sh
    python create_multisig.py
    python mine_block.py
    ```

---

## Project Structure
