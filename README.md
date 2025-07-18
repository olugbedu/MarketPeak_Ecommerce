# AWS IAM Project - Security & Identity Management

## Project Overview

This project demonstrates the implementation of AWS Identity and Access Management (IAM) for a fictional fintech startup called **Zippy e-Bank**. The project focuses on creating secure access controls for different user roles while following the principle of least privilege.

**Duration:** 2 hours  
**Scenario:** Fintech startup requiring secure cloud resource management

## Prerequisites

- AWS Account with administrator access
- Basic understanding of cloud computing principles
- Access to AWS Management Console

## Project Objectives

By completing this project, you will:

1. Understand AWS IAM fundamentals (users, groups, roles, policies)
2. Apply IAM concepts to secure a fintech startup's cloud infrastructure
3. Develop practical skills using the AWS Management Console
4. Implement multi-factor authentication (MFA) for enhanced security
5. Validate access controls and group policies

## Architecture Overview

The project creates IAM resources for two distinct roles:
- **Backend Developer (John)**: Requires EC2 access for server management
- **Data Analyst (Mary)**: Requires S3 access for data storage and analysis

## Implementation Steps

### Step 1: Initial Setup

1. **Access AWS Console**
   - Log in to AWS Management Console using administrator credentials
   - Navigate to IAM Dashboard

2. **Project Context**
   - Working with Zippy e-Bank (fictional fintech startup)
   - Need to create secure access for expanding team (10 developers + 5 analysts)

### Step 2: Create IAM Policies

#### 2.1 Development Team Policy

1. Navigate to IAM Console → Policies
2. Click "Create Policy"
3. Select Service: Search for "EC2"
4. Permissions: Select "All EC2 actions"
5. Resources: Select "All"
6. Click "Next"
7. Policy Details:
   - Name: `developers`
   - Description: "Policy for backend developers requiring EC2 access"
8. Click "Create Policy"

#### 2.2 Data Analyst Team Policy

1. Repeat the process above with these changes:
   - Service: Search for "S3"
   - Permissions: Select "All S3 actions"
   - Policy Name: `analyst`
   - Description: "Policy for data analysts requiring S3 access"

### Step 3: Create IAM Groups

#### 3.1 Development Team Group

1. Navigate to IAM Console → User Groups
2. Click "Create Group"
3. Group Configuration:
   - Name: `Development-Team`
   - Description: "Group for backend developers"
4. Attach Policy: Select the `developers` policy created earlier
5. Click "Create Group"

#### 3.2 Data Analyst Team Group

1. Repeat the process above with these changes:
   - Name: `Analyst-Team`
   - Description: "Group for data analysts"
   - Attach Policy: Select the `analyst` policy

### Step 4: Create IAM Users

#### 4.1 Create User for John (Backend Developer)

1. Navigate to IAM Dashboard → Users
2. Click "Create User"
3. User Configuration:
   - Username: `John`
   - Access Type: Enable "AWS Management Console access"
4. Permissions: Add user to `Development-Team` group
5. Click "Create User"
6. **Important**: Download login credentials for John

#### 4.2 Create User for Mary (Data Analyst)

1. Repeat the process above with these changes:
   - Username: `Mary`
   - Group: Add to `Analyst-Team` group
2. Download login credentials for Mary

### Step 5: Testing and Validation

#### 5.1 Test John's Access

1. **Login Test**:
   - Use John's credentials to log into AWS Console
   - Verify successful authentication

2. **EC2 Access Test**:
   - Navigate to EC2 Dashboard
   - Attempt to view/launch EC2 instances
   - Confirm appropriate permissions

3. **Access Restriction Test**:
   - Try accessing S3 (should be denied)
   - Verify principle of least privilege

#### 5.2 Test Mary's Access

1. **Login Test**:
   - Use Mary's credentials to log into AWS Console
   - Verify successful authentication

2. **S3 Access Test**:
   - Navigate to S3 Dashboard
   - Attempt to create/manage S3 buckets
   - Confirm appropriate permissions

3. **Access Restriction Test**:
   - Try accessing EC2 (should be denied)
   - Verify principle of least privilege

### Step 6: Implement Multi-Factor Authentication (MFA)

#### 6.1 Setup MFA for John

1. **Prerequisites**:
   - Install Google Authenticator or Microsoft Authenticator on mobile device

2. **Configuration Steps**:
   - Navigate to IAM → Users → John
   - Click "Enable MFA"
   - Device name: `John-MFA-Device`
   - Select "Authenticator app"
   - Click "Next"

3. **App Configuration**:
   - Open authenticator app on mobile device
   - Scan QR code displayed in AWS console
   - Enter two consecutive codes from the app
   - Complete MFA setup

#### 6.2 Setup MFA for Mary

1. Repeat the same process for Mary:
   - Device name: `Mary-MFA-Device`
   - Follow identical steps as John's setup

### Step 7: Validation of Group Policies

1. **Access Verification**:
   - Confirm John can only access EC2 resources
   - Confirm Mary can only access S3 resources
   - Verify neither user can access unauthorized services

2. **Security Validation**:
   - Test MFA requirement for both users
   - Confirm enhanced security layer is active
   - Validate adherence to least privilege principle

## Project Results

### Successfully Created:

- ✅ 2 Custom IAM Policies (`developers`, `analyst`)
- ✅ 2 IAM Groups (`Development-Team`, `Analyst-Team`)
- ✅ 2 IAM Users (`John`, `Mary`)
- ✅ MFA enabled for both users
- ✅ Role-based access controls implemented
- ✅ Security best practices applied

### Key Achievements:

1. **Principle of Least Privilege**: Each user has minimal necessary permissions
2. **Role-Based Access**: Users organized by job function
3. **Enhanced Security**: MFA implementation adds extra protection layer
4. **Scalability**: Group-based approach supports team expansion
5. **Compliance**: Meets fintech security requirements

## Security Considerations

- **Access Control**: Users can only access resources required for their roles
- **Multi-Factor Authentication**: Additional security layer beyond username/password
- **Policy Management**: Centralized control through group-based policies
- **Audit Trail**: All IAM actions are logged for compliance

## Troubleshooting

### Common Issues:

1. **Policy Attachment Issues**:
   - Ensure policies are properly attached to groups
   - Verify group membership for users

2. **MFA Setup Problems**:
   - Check time synchronization on mobile device
   - Ensure authenticator app is properly configured

3. **Access Denied Errors**:
   - Verify user is in correct group
   - Check policy permissions

## Future Enhancements

1. **Role-Based Access Control (RBAC)**: Implement IAM roles for cross-account access
2. **Password Policy**: Implement strong password requirements
3. **Access Keys**: Create and manage programmatic access keys
4. **CloudTrail Integration**: Enhanced logging and monitoring
5. **Automated User Provisioning**: Streamline user creation process

## Conclusion

This project successfully demonstrates the implementation of AWS IAM for a fintech startup, showcasing:

- Proper user and group management
- Policy-based access control
- Multi-factor authentication
- Security best practices
- Scalable architecture for team growth

The implementation ensures that Zippy e-Bank's cloud resources are secure, accessible to authorized personnel only, and compliant with financial industry security standards.

## Additional Resources

- [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
- [AWS Security Best Practices](https://aws.amazon.com/architecture/security-identity-compliance/)
- [IAM Policy Language Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html)