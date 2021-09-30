# Key Management Service KMS

- Service to manage encryption keys for your data on AWS
- Integrated for seamless use with many AWS services
- Simple to encrypt data with keys you manage
- When to use:
  - Whenever working with sensitive data
  - Customer Data
  - Financial Data
  - Secrets
  - Credentials
- Integrates with:
  - S3
  - RDS
  - DynamoDB
  - Lambda
  - EBS
  - EFS
  - CloudTrail (know who has been using keys and accessing data)
  - Developer Tools

## CMK

- Customer Master Key
  - Can Encrypt and decrypt data up to 4KB
  - Used to generate encrypt and decrupt Data Ke
- Data Key
  - Used to encrypt data
- Known as Envelope Encryption

- Symmetric Keys
  - Single key for both encrypt and decrypt
- Asymetric Keys
  - Public and private keypair that can be used for encrypt/decrypt or sign/verify
  - If you want people outside your AWS IAM to use you will need to use public key in Asymetric

### CMK Exam tips

- Can use Alias to refer to CMK
- Has Creation Date
- Has description
- Has Key State (Enabled, Disabled, Pending, Deletion, Unavaible)
- Key Material (Customer Provided, KMS Provided)
- Stays Inside KMS

- Setting up CMK (Alias --> Description --> Key Material)
- Key Adminstration Permissions (Users --> Roles --> Admin Permissions)
  - Users and roles who can administer key
- Key Usage Permissions (Users --> Roles --> Admin Permission)
  - users and roles who will use key

- AWS-Managed CMK
  - Created by AWS for interaction with AWS services
- Customer-Manged CMK
  - Keys created and managed by users

- DataKey
  - Used to encrypt and decrypt data
  - Can be generated from CMK

### KMS API Calls

- `aws kms encrypt`
  - cant take name of file to encrypt
  - output name to put encrypted file
  - creates a sipher text output
- `aws kms decrypt`
  - used to decrypt encrypted file
  - decrypts cipher text back to plain text
- `aws kms re-encrypt`
  - allows rotation of encrypted files keys
  - decrypts then re-encrypts with new key
- `aws kms enable-key-rotation`
  - Allows AWS to rotate your key on annual basis
- `aws kms generate-data-key`
  - Creates a data key so you can encrypt data above 4KB

### Envelope Encryption

- Process for encrypting your data
  - for files over 4KB in size
- How to get one
  - Use CMK to generate Data-key
- Why use it
  - Network
    - When you encrypt data directly with KMS it must be transferred over the network
  - Performance
    - With envelope encryption, only the data key goes over the netwoek not your data
  - Benefits
    - The data key is used locally in your application or AWS servic. Avoiding the need to transfer large amounts of data to KMS
  