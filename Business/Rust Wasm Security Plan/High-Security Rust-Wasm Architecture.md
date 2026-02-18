## Metadata

- **Project Type:** Rust / WebAssembly
    
- **Pattern:** Adapter / Virtual Workspace
    
- **Security Level:** High (PII/FHIR Isolation)
    
- **Status:** 🛠️ Implementation Guide
    

---

## 🏗️ Architectural Overview

Using a **Virtual Workspace** allows us to decouple "Pure Rust" logic from "Wasm Glue" code. This ensures the core logic remains platform-agnostic, testable, and reusable in CLI or Mobile environments.

> [!abstract] Key Benefits
> 
> - **Portability:** Core logic can be used in a CLI or Native app without Wasm bloat.
>     
> - **Testability:** Run `cargo test` on the core logic without a Wasm sandbox.
>     
> - **Isolation:** The `wasm-bindgen` dependencies are contained strictly within the adapter crate.
>     

---

## 🚀 Implementation Steps

### Step 1: Initialize the Virtual Workspace Root

A virtual workspace manages member crates without having a root package of its own.

Bash

```
mkdir security-core-project && cd security-core-project
touch Cargo.toml
```

**Root `Cargo.toml`:**

Ini, TOML

```
[workspace]
resolver = "2"
members = [
    "crates/core",
    "crates/wasm",
]
```

---

### Step 2: Create the Core Logic Crate

This crate handles PII masking and FHIR validation. It has **zero** knowledge of WebAssembly.

Bash

```
mkdir -p crates/core
cargo init crates/core --lib
```

**`crates/core/Cargo.toml`:**

Ini, TOML

```
[package]
name = "high-security-core"
version = "0.1.0"
edition = "2021"

[lib]
crate-type = ["rlib"]

[dependencies]
serde = { version = "1.0", features = ["derive"] }
regex = "1.10"
```

---

### Step 3: Create the Wasm Bridge (The Adapter)

This serves as the bridge between Rust and TypeScript.

Bash

```
mkdir -p crates/wasm
cargo init crates/wasm --lib
```

**`crates/wasm/Cargo.toml`:**

Ini, TOML

```
[package]
name = "wasm-bridge"
version = "0.1.0"
edition = "2021"

[lib]
# cdylib produces the .wasm file; rlib is for internal testing
crate-type = ["cdylib", "rlib"]

[dependencies]
wasm-bindgen = "0.2"
serde-wasm-bindgen = "0.6" 
high-security-core = { path = "../core" }
```

---

### Step 4: Implement the Adapter Pattern

#### 1. Pure Logic (`crates/core/src/lib.rs`)

Rust

```
pub struct SecurityEngine {
    mask_pattern: String,
}

impl SecurityEngine {
    pub fn new(pattern: &str) -> Self {
        Self { mask_pattern: pattern.to_string() }
    }

    pub fn mask_data(&self, input: &str) -> String {
        // Pure Rust implementation using regex
        input.replace(&self.mask_pattern, "***")
    }
}
```

#### 2. Wasm Adapter (`crates/wasm/src/lib.rs`)

Rust

```
use wasm_bindgen::prelude::*;
use high_security_core::SecurityEngine;

#[wasm_bindgen]
pub struct WasmSecurityAdapter {
    inner: SecurityEngine,
}

#[wasm_bindgen]
impl WasmSecurityAdapter {
    #[wasm_bindgen(constructor)]
    pub fn new(pattern: &str) -> Self {
        Self {
            inner: SecurityEngine::new(pattern),
        }
    }

    pub fn process_masking(&self, input: &str) -> String {
        // Translates types or handles Wasm-specific requirements
        self.inner.mask_data(input)
    }
}
```

---

### Step 5: Build and Verify

Navigate to your Wasm bridge directory to build the package for your frontend.

Bash

```
cd crates/wasm
wasm-pack build --target web
```

---

## 🔍 Validation Checklist

- [ ] `cargo test -p high-security-core` (Native tests pass)
    
- [ ] `wasm-pack build` (Wasm binary generates successfully)
    
- [ ] `crates/core` contains no `wasm-bindgen` imports