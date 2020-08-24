## AWS Key Management Service

## Use cases

- Allows encryption of data.

## Components

- Customer Master Keys
  - Control access to Data Encryption Keys for encryption/decryption.
  - Types
    - Customer Managed CMK - you create, own and manage them.
    - AWS Managed CMK - owned and managed by AWS. Used in the account only.
    - AWS Owned CMK - owned and managed by AWS. Used in all services
- Data Encryption Keys
  - Used to encrypt the actual data (large amounts).
  - Created by CMKs, 128 or 256 bit sizes.
- Envelope ecncryption - encrypts plaintext data with DEK, then encrypts the DEK with a master key.
- Key policies - define who can use and manage a CMK.
- Grants - also grant AWS principals access to the CMK.
  - Grant token allows for immediate use of the CMK.
- CMK aliases can identify a single CMK under multiple names.

## Integration

- CloudTrail provides access of key usage on resources.
- Automatic key rotation - happens every year, keep copies of CMKs to decrypt past data.

## Metrics

## Pricing

- Customer CMKs - have monthly and usage fees, outside of the free tier.
- AWS managed CMKs - have no monthly fee, but have usage fees outside of the free tier.
- AWS Owned CMKs - no fees.
