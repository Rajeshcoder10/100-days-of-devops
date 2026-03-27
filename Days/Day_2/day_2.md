# Day 2: Temporary User Setup with Expiry Date | 100 Days of DevOps

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/1_task.png" alt="Image">
</div>

## 🎯 Content:
> Today I worked on setting up a Temporary User Setup with Expiry Date as part of my 100 Days of DevOps journey.
> 
> Useful to Automatically disable accounts after specified date.

## What I Learned

*   How to create a user with a Expiry Date
    
*   Temporary Account Management
    
    
## Task Details

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/2_task details.png" alt="Image">
</div>

## Steps I Followed

### 1\. Connect to the server

```plaintext
ssh user@server-name
```

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/3_ssh.png" alt="Image">
</div>

### 2\. Create a user with expiry date

```plaintext
sudo useradd -m -e 2026-12-07 tempuser
```
### Explanation:

- `-m` → creates a home directory (`/home/tempuser`)
- `-e YYYY-MM-DD` → sets the account expiry date
- `tempuser` → username


### 3\. Verify user creation

```plaintext
cat /etc/passwd
```

Check if the new user appears in the list.
<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/4_user check.png" alt="Image">
</div>

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/4_user result.png" alt="Image">
</div>

### 4\. Verify Expiry Date

Use the `chage` command:

>**`chage` command** is used to manage and view user account expiration and password aging information in Linux. 
>

>It helps administrators set expiry dates, enforce password changes, and check account validity.
>

```plaintext
sudo chage -l tempuser
```

Look for:

```plaintext
Account expires : Apr 01, 2026
```

<div style="border:1px solid #ccc; padding:10px; border-radius:10px; box-shadow:2px 2px 8px rgba(0,0,0,0.2); display:inline-block;">
  <img src="./images/5_user expiry details.png" alt="Image">
</div>

### My Understanding

### Purpose of Setting Up a Temporary User in Linux

Creating a temporary user account is useful when you need to provide **limited-time access** to a system without affecting long-term security or user management.

**Common purposes:**
- 👨‍💻 **Short-term access** for interns, contractors, or guest users  
- 🔧 **Testing and troubleshooting** without using permanent accounts  
- 🔐 **Security control** by automatically disabling access after a set date  
- 📂 **Isolated work environment** to prevent interference with other users  
- 🧪 **Training or demo sessions** where accounts are only needed temporarily  

This approach helps maintain system security while keeping user management clean and organized.

* * *

### Topics Covered

- ***Temporary Account Management***
- ***User Management***

**Previous Task**: [Day_1 - Linux User Setup with Non-Interactive Shell](../Day_1/day_1.md)

**Next Task**: [Day_3 - Secure Root SSH Access](../Day_3/day_3.md)