# Runbook: CloudTrail Tampering

This runbook explains how to investigate CloudTrail logging changes, including disabled, deleted, or modified trails.

## 1. Related Rules

```text
AWS CloudTrail Logging Disabled or Modified
```

## 2. Why This Alert Matters

CloudTrail is a core AWS security log source. If logging is disabled or modified, an attacker may be attempting to hide activity.

## 3. Initial Triage

Review these fields first:

```text
@timestamp
event.action
event.provider
event.outcome
cloud.account.id
cloud.region
source.ip
user_agent.original
aws.cloudtrail.user_identity.type
aws.cloudtrail.user_identity.arn
aws.cloudtrail.error_code
aws.cloudtrail.error_message
aws.cloudtrail.request_parameters
```

## 4. Elastic Queries

Main CloudTrail query:

```kql
data_stream.dataset:"aws.cloudtrail"
```

Focused query:

```kql
data_stream.dataset:"aws.cloudtrail" and event.provider:"cloudtrail.amazonaws.com"
```

## 5. Investigation Steps

1. Identify the AWS identity involved.
2. Check the source IP address.
3. Check the user agent.
4. Review the exact AWS API action.
5. Confirm whether the activity was approved.
6. Search for activity from the same identity before and after the alert.
7. Check for related IAM, S3, CloudTrail, KMS, or Organizations activity.
8. Record all evidence and screenshots.

## 6. Containment

If the activity is suspicious:

1. Disable or rotate affected credentials.
2. Revoke unnecessary permissions.
3. Restore secure configuration.
4. Review recent CloudTrail activity.
5. Preserve evidence.
6. Escalate if required.

## 7. Recovery

1. Confirm the affected AWS service is secure.
2. Confirm Elastic is still receiving logs.
3. Confirm detection rules are enabled.
4. Remove temporary test users or keys.
5. Update documentation with the final result.

## 8. Evidence Checklist

```text
Alert screenshot: To update
Raw CloudTrail event screenshot: To update
AWS identity reviewed: To update
Source IP reviewed: To update
Response action completed: To update
Final decision: To update
```
