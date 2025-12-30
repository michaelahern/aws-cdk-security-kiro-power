---
inclusion: always
---

AWS KMS Configuration Requirements

# Configure KMS Keys on Supported AWS CDK Resources

 * AWS KMS keys must be used to encrypt data at rest. This is a requirement for all AWS services that support storing customer data.
 * Specifically, explicitly created and managed KMS Customer Managed Keys (CMKs) should be used where possible.
 * Encryption managed by AWS, sometimes referred as AWS or S3 managed encryption, is not sufficient.
 * Check CDK documentation and source code for properties that support cdk.aws_kms.Key resources, typically named `encryptionKey` or similar.

## Samples

This is not a comprehensive list of all resources that support KMS encryption, but rather a sample of resources that support KMS encryption.

Secrets Manager

```typescript Secrets Manager
  // Good! [Server Side Encryption: AWS KMS Customer Managed Key]
  new secretsmanager.Secret(this, 'SampleSecret', {
    secretName: 'Sample',
    encryptionKey: new cdk.aws_kms.Key(this, 'SecretSecretKey', { }),
    // ...
  });

  // Bad! [No Encryption]
  new secretsmanager.Secret(this, 'SampleSecret', {
    secretName: 'Sample',
    // ...
  });
```

S3

```typescript S3
  // Good! [Server Side Encryption: AWS KMS Customer Managed Key]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    encryption: s3.BucketEncryption.KMS,
    encryptionKey: new cdk.aws_kms.Key(this, 'SampleBucketKey', { }),
    // ...
  });

  // Bad! [No Encryption]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    // ...
  });

  // Bad! [Server Side Encryption: AWS Managed KMS Key]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    encryption: s3.BucketEncryption.KMS_MANAGED,
    // ...
  });

  // Bad! [Server Side Encryption: S3 Managed]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    encryption: s3.BucketEncryption.S3_MANAGED,
    // ...
  });
```
