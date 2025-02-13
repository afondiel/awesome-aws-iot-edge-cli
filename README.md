[![](https://img.shields.io/badge/Contribute-Welcome-green)](#)

# Awesome AWS IoT & Edge CLI (v2)

## Overview

This reference covers essential commands for AWS IoT & Edge device management, data operations, using AWS CLI v2.

## Table of Contents
- [Installation & Configuration Requirements](#installation--configuration-requirements)
- [Core IoT Services](#core-iot-services)
- [Device Management Commands](#device-management-commands)
- [Data Plane Operations](#data-plane-operations)
- [Greengrass Integration](#greengrass-integration)
- [Advanced Features](#advanced-features)
- [Troubleshooting Essentials](#troubleshooting-essentials)
- [References](#references)

## Installation & Configuration Requirements
### Installation Guide
- Please refer to this [guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html).

### Configuration Setup
- AWS Credentials with `AWSIoTDataAccess`
- CLI v2.2+ for latest IoT features
- Python 3.7+ runtime environment

## Core IoT Services

### Thing Registry Management
- **`aws iot create-thing`**: Creates a new IoT device entry in the registry  
  ```
  aws iot create-thing --thing-name MySensor
  ```
- **`aws iot list-things`**: Lists all registered IoT devices 
- **`aws iot describe-thing`**: Shows detailed configuration of a specific device  
- **`aws iot update-thing`**: Modifies device attributes and metadata

### Certificate Operations
- **`aws iot create-keys-and-certificate`**: Generates X.509 certificates for device authentication  
- **`aws iot register-certificate`**: Links certificates to IoT devices

### Policy Management
- **`aws iot create-policy`**: Defines access control rules  
  ```
  aws iot create-policy --policy-name SensorAccess --policy-document file://policy.json
  ```
- **`aws iot attach-policy`**: Assigns policies to certificates

### Rule Engine Configuration
- **`aws iot create-topic-rule`**: Sets up data processing pipelines  
  ```
  aws iot create-topic-rule --rule-name TempAlert --topic-payload file://rule-config.json
  ```
- **`aws iot list-topic-rules`**: Displays all active rules

## Device Management Commands

### Remote Operations
- **`aws iot list-commands`**: Shows queued device commands  
- **`aws iot cancel-command`**: Aborts pending device operations 
- **`aws iot describe-job`**: Checks status of device firmware updates

### Shadow Operations
- **`aws iot-data get-thing-shadow`**: Retrieves device state information  
  ```
  aws iot-data get-thing-shadow --thing-name MySensor shadow.json
  ```
- **`aws iot-data update-thing-shadow`**: Modifies device shadow state 

## Data Plane Operations

### Message Broker
- **`aws iot-data publish`**: Sends messages to IoT topics  
  ```
  aws iot-data publish --topic sensors/temp --payload '{"value":25}'[7]
  ```
- **`aws iot describe-endpoint`**: Gets custom IoT data endpoint 
  ```
  aws iot describe-endpoint --endpoint-type iot:Data-ATS
  ```

### Batch Processing
- **`aws iot batch-associate-thing-with-think-group`**: Bulk device grouping  
- **`aws iot batch-update-thing`**: Mass device configuration updates

## Greengrass Integration

### Local Device Management
- **`greengrass-cli deployment create`**: Deploys components to edge devices  
- **`greengrass-cli component list`**: Shows installed components  

### Log Management
- **`greengrass-cli logs retrieve`**: Collects device operation logs  
- **`greengrass-cli component restart`**: Restarts specific services

## Advanced Features

### Security Monitoring
- **`aws iot list-v2-logging-levels`**: Audits security configurations  
- **`aws iot update-security-profile`**: Modifies device security parameters

### Device Metrics
- **`aws iot list-metric-values`**: Retrieves operational telemetry  
- **`aws iot get-statistics`**: Aggregates device performance data

## Troubleshooting Essentials

1. Verify CLI configuration:
   ```
   aws iot list-things --region us-west-2
   ```
2. Check JSON formatting for data commands:
   ```
   aws iot-data publish --topic debug --payload "$(echo '{"status":"ok"}' | jq -c)"
   ```
3. Test Greengrass connectivity:
   ```
   greengrass-cli component versions
   ```

> **Pro Tip**: Use `--query` and `--output` parameters for filtered responses:
> ```
> aws iot list-things --query "things[?thingName=='MySensor']" --output table
> ```

[Back to Top](#table-of-contents)

## References

- [AWS IoT CLI v2 Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/iot/index.html)
  - [AWS IoT examples using AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli_iot_code_examples.html)
  - [Greengrass CLI Guide](https://docs.aws.amazon.com/greengrass/v2/developerguide/gg-cli-reference.html)
  - [AWS CLI - GitHub Repo](https://github.com/aws/aws-cli)
- [AWS IoT Developer Guide](https://docs.aws.amazon.com/iot/latest/developerguide/index.html)
  - [AWS IoT Core API Reference](https://docs.aws.amazon.com/iot/latest/apireference/index.html)
  - [Device Shadow REST API](https://docs.aws.amazon.com/iot/latest/developerguide/device-shadow-rest-api.html)
