---
name: "aws-cdk-security"
displayName: "AWS CDK Security"
description: "Perform AWS CDK Security Reviews"
keywords: ["aws", "cdk"]
author: "Michael Ahern"
---

# AWS CDK Security Review Power

A specialized power for reviewing AWS infrastructure as code, specifically CDK written in TypeScript, conforms to foundational security policy configurations.

## MCP Servers

This power includes the following MCP servers:

### awsknowledge
- **Purpose**: Discover AWS best practices, API documentation, and service announcements
- **Type**: HTTP Server
- **URL**: https://knowledge-mcp.global.api.aws

## Steering Files

The power includes comprehensive steering guidance covering:

### KMS: Encryption at Rest
- Ensure AWS resources are configured to use KMS Customer Managed Keys, where supported, to encrypt data at rest.

### SSL/TLS: Encryption in Transit
- Ensure AWS resources are configured to use TLS 1.2 or higher for secure communication of data in transit.

## Usage

This power is designed to assist with reviewing and validating the secure configurations of AWS CDK defined infrastructure and applying these best practices within CDK projects.
