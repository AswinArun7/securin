
# SECURIN – Blockchain-Based Digital Evidence Integrity System

## Overview

SECURIN is a blockchain-based digital evidence storage and verification system designed to ensure the integrity of legal evidence over long investigation and trial periods. The system avoids centralized databases and instead uses IPFS for decentralized file storage and the Ethereum blockchain for immutable hash storage, enabling reliable tamper detection.

---

## Problem Statement

Digital evidence stored in centralized systems is vulnerable to tampering, unauthorized modification, or silent deletion. Since legal cases often span months or years, proving that evidence has not been altered becomes difficult. Traditional databases cannot provide cryptographic immutability or public verifiability.

---

## Solution

SECURIN solves this problem by:

* Storing evidence files (images, videos, documents) in IPFS
* Storing cryptographic hashes (CIDs) of evidence on the Ethereum blockchain
* Verifying evidence integrity by comparing hashes during later checks

Any modification to the evidence results in a different hash, clearly indicating tampering.

---

## System Architecture

```
Frontend (Flutter / HTML + JS)
        |
        v
FastAPI Backend
        |
        v
IPFS (Evidence Storage)
        |
        v
Ethereum Blockchain (Hash Storage)
```

---

## End-to-End Workflow

### Evidence Upload

* Evidence file and Case/FIR ID are uploaded from the frontend
* Data is sent using HTTPS with multipart/form-data
* Backend receives:

  * Binary data → Evidence file
  * Form data → Case ID / Evidence ID

### IPFS Storage

* Backend uploads the evidence file to IPFS
* IPFS generates a CID (Content Identifier) representing the file

### Blockchain Storage

* Backend calls a Solidity smart contract
* Case ID, Evidence ID, and CID are stored as Solidity state variables
* Communication uses Ethereum JSON-RPC with ABI-encoded calldata

### Verification

* Evidence is re-uploaded for checking
* Backend generates a new CID via IPFS
* Original CID is fetched from the blockchain using a read-only RPC call
* Hashes are compared to determine authenticity

### Result

* Backend returns verification result to the frontend in JSON format

---

## Verification Logic

```
If current CID == blockchain CID
    Evidence is authentic
Else
    Evidence is tampered
```

---

## Technologies Used

### Frontend

* Flutter (evidence upload)
* HTML, CSS, JavaScript (verification interface)
* HTTP / HTTPS

### Backend

* FastAPI (Python)
* IPFS HTTP API
* Ethereum JSON-RPC

### Blockchain

* Ethereum
* Solidity
* ABI encoding

---

## Data Flow: Protocols and Formats

| Stage                | Protocol | Format               |
| -------------------- | -------- | -------------------- |
| Frontend → Backend   | HTTPS    | multipart/form-data  |
| Backend → IPFS       | HTTP     | Binary               |
| Backend → Blockchain | HTTP     | JSON-RPC             |
| Smart Contract Calls | —        | ABI-encoded calldata |
| Backend → Frontend   | HTTPS    | JSON                 |

---

## Database Usage

SECURIN does not use a traditional database for evidence storage.

* Evidence files are stored in IPFS
* Hashes are stored immutably on the blockchain

A database can be optionally added for metadata indexing, user management, and audit logs, without affecting evidence integrity.

---

## Key Features

* Tamper-proof evidence verification
* Decentralized storage using IPFS
* Immutable hash storage on blockchain
* Support for multiple evidence files per Case ID
* Clear verification results for legal use

---

## Future Enhancements

* Role-based access control
* Database for indexing and audit logs
* Wallet-based authentication
* Deployment on public testnets or Layer-2 networks

---

## Key Takeaway

SECURIN ensures long-term digital evidence integrity by combining decentralized storage with blockchain immutability, making any tampering immediately detectable.

---


tell me and I’ll adjust it cleanly.
