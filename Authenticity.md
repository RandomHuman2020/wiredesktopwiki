## Introduction

You can check the authenticity of our Windows wrapper when you compare it's Certificate Fingerprint & File Checksum. These values are listed on our Download page: https://wire.com/download/

**Screenshot**

![Screenshot](https://cloud.githubusercontent.com/assets/469989/17731326/16a10354-646d-11e6-9075-654b9f830fae.png)

## Check File Checksum

- `certUtil -hashfile WireSetup.exe SHA256`

**Screenshot**

![Screenshot](https://cloud.githubusercontent.com/assets/10243309/17216132/a3c19b2e-54df-11e6-871d-d3d15b7b4877.png)

## Check Certificate Fingerprint

The fingerprint does not change unless we use a new certificate. It can be verified using the the certificate details on `WireSetup.exe`:

![Screenshot](https://cloud.githubusercontent.com/assets/10243309/17216060/5ce5ca54-54df-11e6-9238-ad1d4c969164.png)