# AWS IAM Mini Project - Implementation Guide

## Project Overview

This document provides the actual implementation steps and code for completing the AWS IAM mini project, including all CLI commands, JSON policy documents, and validation steps required to demonstrate successful completion.

**Project Duration:** 2 hours  
**Scenario:** GatoGrowFast.com needs IAM access setup for employees Eric, Jack, and Ade

## Part 1: Creating IAM Policy and User for Eric

### Step 1: Create IAM Policy for EC2 Full Access

**CLI Command:**
```bash
aws iam create-policy \
    --policy-name policy_for_eric \
    --policy-document file://ec2-full-access-policy.json \
    --description "Full access to EC2 for Eric"
```

**Policy Document (ec2-full-access-policy.json):**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*"
        }
    ]
}
```

**Expected Output:**
```json
{
    "Policy": {
        "PolicyName": "policy_for_eric",
        "PolicyId": "ANPXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:policy/policy_for_eric",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 0,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "CreateDate": "2025-01-18T10:30:00Z",
        "UpdateDate": "2025-01-18T10:30:00Z"
    }
}
```

### Step 2: Create IAM User Eric

**CLI Command:**
```bash
aws iam create-user --user-name Eric
```

**Expected Output:**
```json
{
    "User": {
        "Path": "/",
        "UserName": "Eric",
        "UserId": "AIDXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:user/Eric",
        "CreateDate": "2025-01-18T10:35:00Z"
    }
}
```

### Step 3: Create Login Profile for Eric

**CLI Command:**
```bash
aws iam create-login-profile \
    --user-name Eric \
    --password TempPassword123! \
    --password-reset-required
```

**Expected Output:**
```json
{
    "LoginProfile": {
        "UserName": "Eric",
        "CreateDate": "2025-01-18T10:36:00Z",
        "PasswordResetRequired": true
    }
}
```

### Step 4: Attach Policy to Eric

**CLI Command:**
```bash
aws iam attach-user-policy \
    --user-name Eric \
    --policy-arn arn:aws:iam::123456789012:policy/policy_for_eric
```

**Validation - List Eric's Attached Policies:**
```bash
aws iam list-attached-user-policies --user-name Eric
```

**Expected Output:**
```json
{
    "AttachedPolicies": [
        {
            "PolicyName": "policy_for_eric",
            "PolicyArn": "arn:aws:iam::123456789012:policy/policy_for_eric"
        }
    ]
}
```

## Part 2: Creating IAM Group and Users for Development Team

### Step 5: Create IAM Group

**CLI Command:**
```bash
aws iam create-group --group-name Development-team
```

**Expected Output:**
```json
{
    "Group": {
        "Path": "/",
        "GroupName": "Development-team",
        "GroupId": "AGPXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:group/Development-team",
        "CreateDate": "2025-01-18T10:40:00Z"
    }
}
```

### Step 6: Create IAM User Jack

**CLI Command:**
```bash
aws iam create-user --user-name Jack
```

**Expected Output:**
```json
{
    "User": {
        "Path": "/",
        "UserName": "Jack",
        "UserId": "AIDXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:user/Jack",
        "CreateDate": "2025-01-18T10:42:00Z"
    }
}
```

### Step 7: Create Login Profile for Jack

**CLI Command:**
```bash
aws iam create-login-profile \
    --user-name Jack \
    --password TempPassword456! \
    --password-reset-required
```

### Step 8: Add Jack to Development Team Group

**CLI Command:**
```bash
aws iam add-user-to-group --group-name Development-team --user-name Jack
```

### Step 9: Create IAM User Ade

**CLI Command:**
```bash
aws iam create-user --user-name Ade
```

**Expected Output:**
```json
{
    "User": {
        "Path": "/",
        "UserName": "Ade",
        "UserId": "AIDXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:user/Ade",
        "CreateDate": "2025-01-18T10:45:00Z"
    }
}
```

### Step 10: Create Login Profile for Ade

**CLI Command:**
```bash
aws iam create-login-profile \
    --user-name Ade \
    --password TempPassword789! \
    --password-reset-required
```

### Step 11: Add Ade to Development Team Group

**CLI Command:**
```bash
aws iam add-user-to-group --group-name Development-team --user-name Ade
```

### Step 12: Create Policy for EC2 and S3 Access

**CLI Command:**
```bash
aws iam create-policy \
    --policy-name development-policy \
    --policy-document file://ec2-s3-full-access-policy.json \
    --description "Full access to EC2 and S3 for Development Team"
```

**Policy Document (ec2-s3-full-access-policy.json):**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:*",
                "s3:*"
            ],
            "Resource": "*"
        }
    ]
}
```

**Expected Output:**
```json
{
    "Policy": {
        "PolicyName": "development-policy",
        "PolicyId": "ANPXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:policy/development-policy",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 0,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "CreateDate": "2025-01-18T10:50:00Z",
        "UpdateDate": "2025-01-18T10:50:00Z"
    }
}
```

### Step 13: Attach Policy to Development Team Group

**CLI Command:**
```bash
aws iam attach-group-policy \
    --group-name Development-team \
    --policy-arn arn:aws:iam::123456789012:policy/development-policy
```

## Validation and Verification

### Verify Group Members

**CLI Command:**
```bash
aws iam get-group --group-name Development-team
```

**Expected Output:**
```json
{
    "Group": {
        "Path": "/",
        "GroupName": "Development-team",
        "GroupId": "AGPXXXXXXXXXXXXXXXXXX",
        "Arn": "arn:aws:iam::123456789012:group/Development-team",
        "CreateDate": "2025-01-18T10:40:00Z"
    },
    "Users": [
        {
            "Path": "/",
            "UserName": "Jack",
            "UserId": "AIDXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:user/Jack",
            "CreateDate": "2025-01-18T10:42:00Z"
        },
        {
            "Path": "/",
            "UserName": "Ade",
            "UserId": "AIDXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:user/Ade",
            "CreateDate": "2025-01-18T10:45:00Z"
        }
    ]
}
```

### Verify Group Policies

**CLI Command:**
```bash
aws iam list-attached-group-policies --group-name Development-team
```

**Expected Output:**
```json
{
    "AttachedPolicies": [
        {
            "PolicyName": "development-policy",
            "PolicyArn": "arn:aws:iam::123456789012:policy/development-policy"
        }
    ]
}
```

### List All Created Users

**CLI Command:**
```bash
aws iam list-users
```

**Expected Output (showing created users):**
```json
{
    "Users": [
        {
            "Path": "/",
            "UserName": "Ade",
            "UserId": "AIDXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:user/Ade",
            "CreateDate": "2025-01-18T10:45:00Z"
        },
        {
            "Path": "/",
            "UserName": "Eric",
            "UserId": "AIDXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:user/Eric",
            "CreateDate": "2025-01-18T10:35:00Z"
        },
        {
            "Path": "/",
            "UserName": "Jack",
            "UserId": "AIDXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:user/Jack",
            "CreateDate": "2025-01-18T10:42:00Z"
        }
    ]
}
```

### List All Created Policies

**CLI Command:**
```bash
aws iam list-policies --scope Local
```

**Expected Output (showing created policies):**
```json
{
    "Policies": [
        {
            "PolicyName": "development-policy",
            "PolicyId": "ANPXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:policy/development-policy",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 1,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2025-01-18T10:50:00Z",
            "UpdateDate": "2025-01-18T10:50:00Z"
        },
        {
            "PolicyName": "policy_for_eric",
            "PolicyId": "ANPXXXXXXXXXXXXXXXXXX",
            "Arn": "arn:aws:iam::123456789012:policy/policy_for_eric",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 1,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2025-01-18T10:30:00Z",
            "UpdateDate": "2025-01-18T10:30:00Z"
        }
    ]
}
```

## Implementation Summary

### Completed Tasks:

1. **✅ IAM Policy for EC2 (Eric):** Created `policy_for_eric` with full EC2 access
2. **✅ IAM User (Eric) Creation:** Created Eric user with login profile and attached EC2 policy
3. **✅ IAM Group (Development-Team):** Created group and added Jack and Ade as members
4. **✅ IAM Policy for EC2 & S3:** Created `development-policy` with full EC2 and S3 access, attached to Development-team group

### Files Created:
- `ec2-full-access-policy.json` - EC2 policy for Eric
- `ec2-s3-full-access-policy.json` - EC2 and S3 policy for Development team

### Access Summary:
- **Eric:** Individual user with EC2 full access
- **Jack:** Member of Development-team group with EC2 and S3 full access
- **Ade:** Member of Development-team group with EC2 and S3 full access

All users have console access with temporary passwords requiring reset on first login.

## Clean-up Commands (Optional)

To remove all created resources:

```bash
# Detach policies
aws iam detach-user-policy --user-name Eric --policy-arn arn:aws:iam::123456789012:policy/policy_for_eric
aws iam detach-group-policy --group-name Development-team --policy-arn arn:aws:iam::123456789012:policy/development-policy

# Remove users from group
aws iam remove-user-from-group --group-name Development-team --user-name Jack
aws iam remove-user-from-group --group-name Development-team --user-name Ade

# Delete login profiles
aws iam delete-login-profile --user-name Eric
aws iam delete-login-profile --user-name Jack
aws iam delete-login-profile --user-name Ade

# Delete users
aws iam delete-user --user-name Eric
aws iam delete-user --user-name Jack
aws iam delete-user --user-name Ade

# Delete group
aws iam delete-group --group-name Development-team

# Delete policies
aws iam delete-policy --policy-arn arn:aws:iam::123456789012:policy/policy_for_eric
aws iam delete-policy --policy-arn arn:aws:iam::123456789012:policy/development-policy
```