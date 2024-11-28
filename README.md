# Noir Circuits Demo with Barretenberg

This repository demonstrates how to create and use zero-knowledge circuits using Noir programming language with Barretenberg as the proving backend. Noir is a Domain Specific Language for writing zero-knowledge proofs, making it easier for developers to create and verify ZK circuits.

## Overview

This project serves as a practical guide to:
- Writing zero-knowledge circuits in Noir
- Compiling and proving circuits using Barretenberg backend
- Verifying proofs generated from Noir circuits

## Project Structure
.
├── src/              # Main directory containing Noir circuits
│   └── main.nr       # Main circuit implementation (circuit entry point)
├── Prover.toml       # Prover inputs configuration
├── Nargo.toml        # Noir project configuration
└── README.md         # Project documentation

## Prerequisites

Before getting started, follow the [Noir Quick Start Guide](https://noir-lang.org/docs/getting_started/quick_start) to install:
- Noir and Nargo (using `noirup`)
- Barretenberg proving backend (using `bbup`)

> **Note for Windows Users**: Barretenberg currently doesn't provide Windows binaries. It's recommended to use Windows Subsystem for Linux (WSL) for development.

## Getting Started

1. Clone the repository:
```bash
git clone <repository-url>
cd noir-demo
```

2. Generate the Prover.toml file:
```bash
nargo check
```

3. Compile and execute the Noir program:
```bash
nargo execute
```

This will generate the witness and artifact files in the `target` folder.

4. Generate the proof using Barretenberg:
```bash
bb prove -b $PATH_ARTIFACT -w $PATH_WITNESS -o $PATH_PROOF
```

5. Generate the verification key:
```bash
bb write_vk -b $PATH_ARTIFACT -o $PATH_VK
```

6. Verify the proof:
```bash
bb verify -k $PATH_VK -p $PATH_PROOF
```

> Note: Replace `$PATH_ARTIFACT`, `$PATH_WITNESS`, `$PATH_PROOF`, and `$PATH_VK` with the actual paths to your files:
> - `$PATH_ARTIFACT`: Usually `target/noir-demo.json`
> - `$PATH_WITNESS`: Usually `target/noir-demo.gz`
> - `$PATH_PROOF`: Your desired proof output path (e.g., `target/proof`)
> - `$PATH_VK`: Your desired verification key path (e.g., `target/vk`)

## Working with Inputs

1. The circuit inputs are configured in `Prover.toml`. You can modify this file to test different input values.

2. Example `Prover.toml`:
```toml
x = 1
y = 2
```

## Circuit Details

The main circuit is located in `src/main.nr`. This is where the zero-knowledge proof logic is implemented.