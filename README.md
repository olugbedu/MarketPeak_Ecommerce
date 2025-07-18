# AWS IAM Management Automation – Shell Script

## Project Overview

CloudOps Solutions has adopted AWS to manage its cloud infrastructure. As part of its growth strategy, the company wants to **automate AWS IAM (Identity and Access Management)** operations for onboarding DevOps team members. This project focuses on developing a **shell script** to manage IAM users, groups, and policies using the AWS CLI.

---

## Objectives

The script was extended to accomplish the following tasks:

1. Define an array of IAM usernames.
2. Create IAM users from the array.
3. Create an IAM group named `admins`.
4. Attach the `AdministratorAccess` AWS-managed policy to the group.
5. Add all users to the `admins` group.

---

## Pre-requisites

Before running the script:

- Ensure **AWS CLI** is installed and configured (`aws configure`).
- Use an IAM identity with appropriate permissions to manage users, groups, and policies.
- Have **Linux shell scripting basics** and prior mini-projects completed.

---

## Script Breakdown

### 1. **IAM User Array Definition**

An array was created to store multiple IAM usernames for easy iteration:

```bash
IAM_USER_NAMES=("devops1" "devops2" "devops3" "devops4" "devops5")
```

---

### 2. **Function: `create_iam_users`**

This function loops over the array and creates each user:

```bash
create_iam_users() {
    echo "Starting IAM user creation process..."
    for username in "${IAM_USER_NAMES[@]}"; do
        aws iam create-user --user-name "$username"
        echo "Created user: $username"
    done
    echo "IAM user creation process completed."
}
```

---

### 3. **Function: `create_admin_group`**

This function checks if the `admins` group exists, creates it if not, and attaches the `AdministratorAccess` policy:

```bash
create_admin_group() {
    echo "Creating admin group and attaching policy..."
    if ! aws iam get-group --group-name "admins" &>/dev/null; then
        aws iam create-group --group-name "admins"
        echo "Group 'admins' created."
    else
        echo "Group 'admins' already exists."
    fi

    aws iam attach-group-policy         --group-name "admins"         --policy-arn "arn:aws:iam::aws:policy/AdministratorAccess"

    echo "Success: AdministratorAccess policy attached to 'admins'."
}
```

---

### 4. **Function: `add_users_to_admin_group`**

This function adds each user to the `admins` group:

```bash
add_users_to_admin_group() {
    echo "Adding users to admin group..."
    for username in "${IAM_USER_NAMES[@]}"; do
        aws iam add-user-to-group --group-name "admins" --user-name "$username"
        echo "Added $username to 'admins' group."
    done
    echo "User group assignment completed."
}
```

---

### 5. **Main Execution Flow**

The `main` function checks for AWS CLI and executes all IAM management tasks:

```bash
main() {
    echo "AWS IAM Management Script"
    if ! command -v aws &>/dev/null; then
        echo "Error: AWS CLI is not installed. Please install and configure it first."
        exit 1
    fi

    create_iam_users
    create_admin_group
    add_users_to_admin_group

    echo "AWS IAM Management Complete!"
}
```

The script ends with:

```bash
main
exit 0
```

---

## Result

By running the script:

- Five IAM users are created.
- An `admins` group is created (if not already existing).
- The `AdministratorAccess` policy is attached to the group.
- All users are added to the group, inheriting admin privileges.

---

## Deliverables

- ✅ Full shell script implementing all objectives
- ✅ Comprehensive documentation of the development process (this README)
- ✅ Script is reusable, idempotent, and properly handles existing resources

---

## Key Commands Used

| Command | Description |
|--------|-------------|
| `aws iam create-user` | Create a new IAM user |
| `aws iam create-group` | Create an IAM group |
| `aws iam attach-group-policy` | Attach a policy to a group |
| `aws iam add-user-to-group` | Add a user to a group |
| `aws iam get-group` | Check if group exists |
| `command -v aws` | Check if AWS CLI is installed |

---

## Final Thoughts

This automation exercise demonstrates how to manage IAM resources efficiently using shell scripting and AWS CLI. Automating user and group creation ensures a consistent and secure way to onboard users in a cloud environment.

---