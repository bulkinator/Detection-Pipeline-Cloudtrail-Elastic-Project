# Test Results

This file records the testing evidence for the CloudTrail to Elastic detection pipeline.

## 1. Test Environment

```text
Project: CloudTrail to Elastic Detection Pipeline
AWS Region: ap-southeast-2
Elastic Dataset: aws.cloudtrail
CloudTrail Source: S3 bucket with .gz CloudTrail logs
Ingestion Method: Elastic AWS integration using S3/SQS
Tester: To update
Test Date: To update
AWS Account ID: To update
```

## 2. Main Elastic Query

```kql
data_stream.dataset:"aws.cloudtrail"
```

## 3. Test Summary

| # | Rule | Test Action | Expected Event | Alert Result |
|---|---|---|---|---|
| 1 | AWS CloudTrail Logging Disabled or Modified | Update or stop/start CloudTrail | UpdateTrail / StopLogging | To update |
| 2 | AccessDenied Spike by Same Identity | Run repeated denied API calls | AccessDenied | To update |
| 3 | AWS API AccessDenied Activity | Run one denied API call | AccessDenied | To update |
| 4 | Root Account Activity | Sign in as root | ConsoleLogin / Root | To update |
| 5 | AWS Console Login Failure | Attempt wrong password | ConsoleLogin Failure | To update |
| 6 | S3 Bucket Public Access or Policy Changed | Modify bucket public access block | PutPublicAccessBlock | To update |
| 7 | Console Login Without MFA | Login without MFA | ConsoleLogin / MFAUsed No | To update |
| 8 | Multiple Failed Console Logins | Fail login several times | ConsoleLogin Failure | To update |
| 9 | IAM Access Key Updated or Deleted | Disable or delete test key | UpdateAccessKey / DeleteAccessKey | To update |
| 10 | S3 Bucket Versioning Changed | Enable or suspend versioning | PutBucketVersioning | To update |

## 4. Evidence Screenshots

![Rules Enabled](../screenshots/rules-enabled.png)

![CloudTrail Events in Discover](../screenshots/discover-cloudtrail-events.png)

![AccessDenied Alert](../screenshots/alert-accessdenied.png)

![Console Login Failure Alert](../screenshots/alert-console-login-failure.png)

![S3 Public Access Alert](../screenshots/alert-s3-public-access.png)

![S3 Versioning Alert](../screenshots/alert-versioning-changed.png)

## 5. Final Result

```text
All 10 AWS CloudTrail detection rules were created and enabled in Elastic Security.

CloudTrail logs were successfully ingested into Elastic using the AWS integration.

Test events were generated in the AWS lab account and reviewed in Elastic Discover.

Alerts were generated successfully for the tested detection scenarios.

Final Status: To update after all screenshots are added.
```
