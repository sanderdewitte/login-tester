# Login Tester

This script automates login testing using real user passwords by interacting with the `login` command via `expect`. It is useful for verifying that password hashes written to `/etc/shadow` (for instance by configuration management tools) work as intended.

## 🔧 Requirements

- Ubuntu or other Linux system with local user accounts
- `expect` installed:
  ```bash
  sudo apt install expect
  ```

- Must be run as root:
  ```bash
  sudo expect ./test_logins.exp
  ```

## 📝 Usage

1. Copy the sample credentials file:
   ```bash
   cp logins.sample logins
   ```

2. Edit the logins file to include your real usernames and passwords (space-separated):
   ```bash
   user1 verysecret123
   user2 verysecret456
   ```

2. Run the script as root:
   ```bash
   sudo expect ./test_logins.exp
   ```

3. Output will look like:
   ```
   🔐 Testing login for user: user1
   ✅ Login succeeded for user1
   🔐 Testing login for user: user2
   ❌ Login failed for user2
   ```

> The script suppresses all MOTD, shell banners, and system output. Only test results are shown.

## ⚠️ Notes

- This does **not** change any passwords or system state.
- This is for **local PAM authentication** only. It does not test SSH, LDAP or other remote login systems.
- Passwords are stored in plain text in the input file, so use with care and only for trusted environments.

## 🔐 Security

- The real logins file is excluded from Git using .gitignore
- Never commit sensitive credentials to the repository

## 📁 Files

- test_logins.exp – The main expect script
- logins.sample – Sample credentials file
- .gitignore – Excludes logins from version control

## 📄 License

MIT License

