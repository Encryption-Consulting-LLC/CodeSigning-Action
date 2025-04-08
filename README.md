# 🔏 CodeSign Secure GitHub Action

Securely sign your software using `signtool` with keys stored in FIPS 140-2 Level 3 compliant HSMs. This action is designed to bring enterprise-grade code signing directly into your DevOps CI/CD pipelines like GitHub Actions.

---

## 🚀 What is Code Signing?

Code Signing ensures the **authenticity** and **integrity** of digital content such as software, scripts, and executables. When a file is signed, the end user can verify that:

- The file has not been altered or tampered with since it was signed.
- It comes from a legitimate source or publisher.

---

## ✅ Key Features

### 🔐 HSM-Backed Keys
- Keys are stored and managed using FIPS 140-2/FIPS 140-3 Level 3 HSMs.
- Cloud-based or on-premises HSM support.
- High security and compliance.

### 🔒 Policy Enforcement & Access Control
- Enforce application-wide signing policies.
- Role-based access and quorum approval (M of N).
- Full audit trail and event logging.

### 🔄 Seamless CI/CD Integration
- Works with GitHub Actions, Jenkins, Azure DevOps, CircleCI, Okta, and more.
- Automates code signing during build/deploy stages.
- Supports client-side hashing for performance.

### 🛡️ Secure Signing Protocols
- RFC 3161 and Authenticode-compliant secure timestamps.
- Supports X.509, OAuth, Basic Auth, and IP filtering.

---

## 🔧 Inputs

| Name              | Description                                 | Required | Default                        |
|-------------------|---------------------------------------------|----------|--------------------------------|
| `file-path`       | Path to the file that needs to be signed    | ✅       | —                              |
| `cert-path`       | Path to the .crt certificate                | ✅       | —                              |
| `key-container`   | Name of the key container                   | ✅       | —                              |
| `timestamp-server`| RFC 3161-compliant timestamp server URL     | ❌       | `http://timestamp.sectigo.com`|

---

## 📁 File Types Supported

- **Windows Authenticode**: `.exe`, `.dll`, `.cab`, `.msi`, `.ps1`, `.sys`, `.ocx`, `.vbs`, `.cat`, `*.msp`, `*.cpl`, `*.efi`, `*.arx`, `*.dbx`, `*.crx`, `*.xsn`, `*.deploy`, `*.xap`, and more.
- **Apple Signing**: `.dmg`, `.ipa`, `.app`, `.pkg`, `.mpkg`
- **Java & Android**: `.jar`, `.apk`, `.war`, `.ear`, `.sar`
- **Firmware**: `.bin`, `.img`, `.hex`, `.fw`, `.dfu`
- **Linux**: `.rpm`, GPG-signed packages, XML
- **Container Signing**: Docker image signing with Docker Notary
- **OVA/OVF**: `.ova`, `.ovf`

---

## 🔐 Use Cases

- Sign Windows installers and updates
- Sign firmware for embedded systems
- Authenticate Java and Android apps
- Sign macOS tools and utilities
- Sign Linux packages for trusted delivery
- Secure Docker/container deployments
- Sign OVA/OVF virtual appliance files

---

## 🧩 Deployment Options

| Model     | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| **Hybrid**| On-prem or cloud-hosted HSMs, keys stored locally or in the cloud           |
| **Cloud** | Deployed in AWS/Azure or private cloud with HSM integration                |
| **On-Prem**| Hosted on servers/containers with local HSMs                               |
| **SaaS**  | Fully managed by Encryption Consulting, including hosted HSMs and APIs     |

---

## 🛠 Example Workflow

```yaml
jobs:
  sign:
    runs-on: [self-hosted, windows]
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Sign file
        uses: Encryption-Consulting-LLC/CodeSigning-Action@v1
        with:
          file-path: 'C:\\CodeSigningFiles\\winsdksetup.exe'
          cert-path: 'C:\\CodeSigningFiles\\ovcodesigningcert.crt'
          key-container: 'ovcodesigningcert'
          timestamp-server: 'http://timestamp.sectigo.com'
