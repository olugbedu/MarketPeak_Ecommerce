# AWS Identity and Access Management (IAM) Mini Project

## Project Overview

This project provides hands-on experience with AWS Identity and Access Management (IAM), focusing on understanding IAM principles, creating and managing IAM policies, users, groups, and roles. The project demonstrates practical implementation of IAM security best practices in a real-world scenario.

**Project Duration:** 2 hours

**Company Scenario:** GatoGrowFast.com (Growth Marketing Consultancy)

## Learning Objectives

By the end of this project, you will be able to:

- Understand AWS Identity and Access Management (IAM) principles and components
- Learn to create and manage IAM policies for regulating access to AWS resources securely
- Apply IAM concepts practically to control access within AWS environments
- Explore best practices for IAM implementation and security in AWS
- Recognize IAM components like users, roles, policies, and groups
- Create and manage IAM policies to define permissions for users and roles
- Set up IAM users, groups, and roles to control access to AWS services
- Understand IAM best practices for maintaining security and managing access to AWS resources

## What is IAM?

IAM, or Identity and Access Management, serves as the gatekeeper for your AWS resources. Its job is to decide who gets in and what they're allowed to do once they're inside.

Think of it as the gatekeeper for your AWS resources - it's job is to decide who gets in and what they're allowed to do once they're inside.

Imagine you have this big digital "house" full of all your AWS stuff - your data, your applications, the whole shebang. Now, you don't want just anyone wandering in and messing around with your things, right? That's where IAM steps in.

It's like having your own VIP list for your digital world. IAM helps you keep your AWS resources safe and sound, making sure only the right people get in and that they're only allowed to do what you say they can. It's all about keeping your digital house in order and protecting your precious stuff from any unwanted guests.

## Key IAM Components

### IAM Users
IAM users are like individual accounts for different people or entities within your AWS environment. Each IAM user would have their own unique username and password, allowing them to access the AWS resources they need for their work.

### IAM Roles
An IAM role defines what someone or something like an application or service can do within your AWS account. Each role has a set of permissions that determine which actions it can perform and which AWS resources it can access.

### IAM Policies
An IAM policy is a set of rules that define what actions a role can take. These rules specify the permissions granted to the role. Think of a policy as a rulebook for the role. It outlines which actions are allowed and which are not, helping to ensure secure and controlled access to your AWS resources, ensuring that only authorized actions are performed by users and roles within your AWS account.

### IAM Groups
IAM Groups are like collections of IAM users. Instead of managing permissions for each user individually, you can organize users into groups based on their roles or responsibilities.

## Project Scenario

A growth marketing consultancy company called GatoGrowFast.com wants to give some access to their employees Eric, Jack and Ade to the AWS resources. Let's see how it is being setup.

We'll do it in Two parts:
1. **Part 1:** Create a policy granting full access to EC2, then create a user named Eric and attach that policy to him.
2. **Part 2:** Create a group and add two more users, Jack and Ade, to that group. Afterward, create a policy for granting full access to EC2 and S3, and attach it to the group.

## Implementation Steps

### Part 1: Creating Individual User Access

#### Step 1: Navigate to AWS Management Console
1. Navigate to the AWS Management Console
2. Use the search bar to locate the Identity and Access Management (IAM) service

#### Step 2: Create IAM Policy
1. On the IAM dashboard, navigate to the left sidebar and click on "Policies"
2. From there, search for "EC2" and select "AmazonEC2FullAccess" from the list of policies
3. Proceed by clicking on "Create policy" to initiate the policy creation process

#### Step 3: Configure EC2 Actions
1. Now, select all EC2 actions

#### Step 4: Create Policy
1. Tick "All resources" and click "Next"
2. Now click on create policy

#### Step 5: Create IAM User
1. Now, proceed to the "Users" section, and select the option to "Create User"

#### Step 6: Configure User Details
1. Enter the desired username for the user
2. Then select the option "Provide user access to the AWS Management Console" if access to the web-based console interface is required
3. Proceed to set up a password for the user
4. Check the box "Users must create a new password at next sign-in" if allowing users to change their password upon first sign-in is preferred

#### Step 7: Attach Policy to User
1. Select "Attach policy directly" and navigate to "Filter customer managed policies"
2. Choose the policy you created named "policy_for_eric"
3. Then proceed by clicking "Next"

#### Step 8: Complete User Creation
1. Ensure to save these details securely for future reference
2. Click on "Return to user list"

**Result:** Eric's user has been successfully created, and the policy granting him full access to EC2 has been attached.

### Part 2: Creating Group-Based Access

#### Step 1: Create User Group
1. On the "User Groups" section, enter a name for the group
2. Click on "Create User Group"
3. Then, proceed to the "Users" section

#### Step 2: Create Additional Users
1. Now, let's create a user named Jack
2. In the "Permissions" options, select "Add user to group"
3. Then, in the "User groups" section, choose the group you created named "development-team"
4. Click "Next"

You need to repeat the same process for user Ade. Create user Ade and add him to the user group "Development-team."

#### Step 3: Create Group Policy
1. Navigate to the "Policies" section and click on "Create Policy" to begin crafting a new policy

#### Step 4: Configure Services
1. Choose the two services, EC2 and S3, from the available options

#### Step 5: Set Policy Details
1. Enter the desired policy name and proceed to click on the "Create policy" button

#### Step 6: Attach Policy to Group
1. Navigate to the "Users group" section and select the "Development-team" group

#### Step 7: Configure Group Permissions
1. Proceed to the "Permissions" section and add the necessary permissions

#### Step 8: Complete Group Setup
1. Click on attach policy

#### Step 9: Select Policy Type
1. Select "Customer Managed Policy" as the policy type
2. Then choose the "development-policy" you created
3. Click "Attach Policy"

**Result:** The policy is now attached to the group, granting full permissions to EC2 and S3 for the group's users.

## AWS Policy Types

### Managed Policies
- **AWS Managed Policies:** Made by AWS, used by many
- **Customer Managed Policies:** You make and manage them

### Inline Policies
- Made for one specific thing

## Best Practices

Based on the project implementation, here are key IAM best practices:

1. **Give only the permissions needed.** Don't give more access than necessary.

2. **Use roles instead of users.** Roles are safer and can be used when needed.

3. **Review roles regularly.** Remove unused roles to keep things tidy and secure.

4. **Add extra security with MFA.** Use Multi-Factor Authentication for extra protection.

5. **Use ready-made policies.** They're safer and easier to use.

6. **Keep policies simple.** Make separate policies for different tasks.

7. **Keep track of changes.** Keep a record of who changes what.

8. **Test policies before using them.** Make sure they work the way you want them to before applying them to real stuff.

9. **Use descriptive names.** Choose clear and descriptive names for IAM groups to facilitate understanding and management.

10. **Enforce strong password policies.** Encourage users to create strong passwords and implement expiration and complexity requirements.

## Additional Security Considerations

### Multi-Factor Authentication (MFA)
For MFA you can check **Multi-Factor Authentication (MFA) for IAM** in IAM documentation.

### Difference Between Users and Roles
- **Users:** Like individual people with their own set of keys to access resources. These keys are permanent and tied to specific individuals. It's similar to having your own key to the front door of your house—it's always yours.

- **Roles:** Like special keys that can be used by different people or even programs. These keys provide temporary access and can be shared among different users for specific tasks.

## Project Reflection

This project demonstrates several key learning outcomes:

- **Understanding IAM:** IAM serves as the security foundation for AWS resources, controlling access and permissions
- **Security Importance:** IAM ensures data protection, compliance, and prevents unauthorized access
- **Policy Creation:** Participants learned to craft IAM policies to regulate resource access effectively
- **Practical Application:** Hands-on exercises equipped participants to set up IAM users, groups, and roles, enhancing their real-world IAM implementation skills

## Conclusion

This mini project provides a comprehensive introduction to AWS IAM fundamentals through practical implementation. By working through both individual user management and group-based access control, participants gain essential skills for securing AWS environments in real-world scenarios.

The hands-on approach ensures understanding of IAM principles while building confidence in managing AWS security effectively.