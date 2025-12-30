---
inclusion: always
---

AWS SSL/TLS Configuration Requirements

# Configure SSL/TLS on Supported AWS CDK Resources

 * On AWS resources that support optionally enabling or disabling SSL/TLS for the encryption of data in transit, the use of SSL/TLS must be enforced.
 * On AWS resources that support specifying SSL/TLS versions and/or cipher suites, the use of TLS 1.2 or higher must be enforced.
 * Check CDK documentation and source code for properties that may expose these configuration options.

## Samples

This is not a comprehensive list of all resources that support enabling/disabling SSL/TLS enforcement, but rather a sample of resources that do.

```typescript S3
  // Good! [SSL Explicitly Enforced]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    enforceSSL: true,
    // ...
  });

  // Bad! [SSL Implicitly Not Enforced (default behavior)]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    // ...
  });

  // Bad! [SSL Explicitly Not Enforced]
  new s3.Bucket(this, 'SampleBucket', {
    bucketName: 'Sample',
    enforceSSL: false,
    // ...
  });
```

```typescript CloudFront
  // Good! [TLS 1.2]
  new cloudfront.Distribution(this, 'Distribution', {
    minimumProtocolVersion: cloudfront.SecurityPolicyProtocol.TLS_V1_2_2021,
    // ...
  });

  // Bad! [TLS 1.1]
  new cloudfront.Distribution(this, 'Distribution', {
    minimumProtocolVersion: cloudfront.SecurityPolicyProtocol.TLS_V1_1_2016,
    // ...
  });
```
