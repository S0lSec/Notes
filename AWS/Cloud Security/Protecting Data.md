# Protect Data at Rest
## Why?
- Information disclosure
- Data integrity compromise
- Accidental or malicious deletion
- System, hardware and software availability
## Data at Rest S3
- S3 data is private by default
- Requires AWS credentials for access
- Use bucket policies for granular access to objects
- Consider encrypting data at rest
## Granting Permissions
**Identity based**
(Attached to an IAM principle)
![[Pasted image 20260513092950.png]]
**Resource based**
(Attached to an AWS resource)
![[Pasted image 20260513092958.png]]
# S3 Protection Features
## Block Public Access
- **BlockPublicAcls**: Block public access granted by new ACLs
- **IgnorePublicAcls**: Block public access granted by any ACLs
- **BlockPublicPolicy**: Block public access granted by new public bucket policies
- **RestrictPublicBuckets**: Block public and cross-account access by any public bucket policies
## S3 Versioning
- Create new version with every upload
- Protects from unintended deletion
- Provides retrieval of deleted objects
- Can be used with lifecycle policies for cost savings
- Cant be turned off once enabled
- Offers multi-factor authentication delete for extra security
## S3 Object Lock
- Stores objects by using WORM model
- Works on in versioned buckets
- Provides the ability to manage object retention
- Provides two retention models:
	- Governance
	- Compliance
# Protection Through Encryption
![[Pasted image 20260513090936.png]]
## Comparing client-side & server-side excryption
**Client-side encryption (CSE)**
- Application encrypts data before sending it to AWS
- Data is stored in its encrypted state
- The keys and algorithms are known only to you
![[Pasted image 20260513091124.png]]
**Server-side encryption (SSE)**
- AWS encrypts data on your behalf after receiving it
- Process is transparent to the user
![[Pasted image 20260513091134.png]]
## Types of S3 server-encryptions
- **SSE-C**
	- Retain control of keys
	- Doesnt store the keys provides
- **SSE-S3**
	- AWS manages keys
	- Encrypted data + keys stored in separate
- **SSE-KMS**
	- AWS manages keys
	- Envelope key is used for added protection
![[Pasted image 20260513091311.png]]
1. You request to open the object.
2. Amazon S3 notices that the requested object is encrypted.
3. Amazon S3 sends the encrypted copy of the data key that the object is encrypted with to AWS KMS.
4. AWS KMS then decrypts the data key by using the customer managed key (which never leaves the AWS KMS service).
5.  AWS KMS then sends the plaintext data key back to Amazon S3.
6. Finally, Amazon S3 decrypts the ciphertext of the data object, allows you to open the object, and deletes the plaintext copy of the data key.
## AWS Key Management Service (KMS)
- Provides ability to create and manage cryptographic keys
- Uses hardware security modules (HSMs) to protect your keys
- Is integrated with other AWS services
- Provides the ability to set usage policies to determine which users can use keys
![[Pasted image 20260513091550.png]]
# Protect Data in Transit
## Why?
- Communications might go through the public internet
- What are the risks that data in transit is exposed to
## Protecting Data in Transit
- Use SSL endpoints over TLS
- Use encryption
- Use VPC endpoints to limit access to your bucket
## Protecting remote connections to servers
- RDP is typically used for Windows servers
	- RDP establishes an underlying SSL/TLS connection
	- For better security issue a trusted X.509 certificate
	- Dont use the default self-signed certificate
- SSH is typically used for Linux servers
	- Established secure connection
	- Use tunneling to protect the application session in transit
	- Don't allow root user to use an SSH terminal
	- Be sure that all users log in with an SSH key pair and then deactivate password authentication
## AWS Certificate Manager (ACM)
- Provides a single interface to manage public + private certificates
- Makes it easy to deploy certificates
- Protects and stores private certificates
- Minimizes downtime and outages with automatic renewals
![[Pasted image 20260513092148.png]]
## ACM Private CA Considerations
- Hardware Security Models (HSMs)
- IAM policies for access control
- Certificate revocation list
- Generated audit reports
# Best Practices
- Generate an S3 Presigned URL and use it to upload files
- A presigned URL uses three parameters to limit user access
- Consider encryption of data at rest and in transit
- Ensure your s3 bucket use of correct policies and are not publicly accessible
- Use principle of least privilege
- Enable MFA delete for buckets
- Enforce encryption for each PUT request
- Set default encryption on a bucket to encrypt all objects
- Use appropriate retention mode if using s3 Object Lock
- Use s3 Block Public Access
- Upload data to S3 over SFTP
- Enable S3 Versioning
# Additional Data Protection Services
## AWS Secrets Manager
- Secure and scalable method for managing access to secrets
- Is a way to meet regulatory and compliance requirements
- Rotates secrets safely without breaking applications
- Audits and monitors the lifecycle of secrets
- Helps you avoid putting secrets in code or config files
![[Pasted image 20260513092734.png]]
## Amazon Macie
- Recognizes sensitive data such as personally identifiable information (PII)
- Allows for custom-defined data types
- Protects data stored in S3 by monitoring resource policies and ACLs
- Provides full API converge for management
- Provides full API coverage for management
- Integrates with AWS Organizations