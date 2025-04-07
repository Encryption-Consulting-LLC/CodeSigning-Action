# 🔏 Code Signing with Encryption Consulting KSP

Digitally sign and verify Windows executables using Microsoft SignTool and the **Encryption Consulting Key Storage Provider (KSP)**. This action is ideal for secure code signing workflows using a non-exportable private key container.

---

![GitHub Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-Code%20Signing%20Action-blue?logo=github)
![Platform](https://img.shields.io/badge/platform-Windows-blue)
![PowerShell](https://img.shields.io/badge/shell-pwsh-blue)

---

## 🚀 Features

- Code signing using `signtool` and EC's Key Storage Provider
- Timestamping with trusted timestamp authorities
- Signature verification using `signtool verify`
- Built for secure environments using self-hosted Windows runners

---

## 📦 Usage

### ✅ Basic Example

```yaml
name: Code Signing and Verification Workflow

on:
  push:
    branches:
      - main

jobs:
  sign-and-verify:
    runs-on: windows-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Run Code Signing Action
        uses: Encryption-Consulting-LLC/CodeSigning-Action@v1
        with:
          file-path: 'C:\\Users\\sam\\Downloads\\ckcerttool.exe'
          cert-path: 'C:\\Users\\sam\\Downloads\\ovcodesigning.crt'
          key-container: 'ovcodesigning'
          timestamp-server: 'http://timestamp.sectigo.com'
