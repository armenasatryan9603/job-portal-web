# How to Add SSH Keys to GitHub

## Your SSH Public Key
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILege+uuQjIm5O4+7nFNGInfvHlk+nJZLc7y1uTr0wyY armen.asatryan@bridgewise.com
```

## Steps to Add SSH Key to GitHub

### Method 1: Using GitHub Web Interface

1. **Copy your public key:**
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   (The key is shown above)

2. **Go to GitHub:**
   - Visit: https://github.com/settings/keys
   - Or: GitHub → Your Profile → Settings → SSH and GPG keys

3. **Add new SSH key:**
   - Click "New SSH key" button
   - **Title**: Give it a name (e.g., "MacBook Pro" or "Work Laptop")
   - **Key**: Paste your public key (the one shown above)
   - **Key type**: Authentication Key (default)
   - Click "Add SSH key"

4. **Verify it works:**
   ```bash
   ssh -T git@github.com
   ```
   You should see: `Hi username! You've successfully authenticated...`

### Method 2: Using GitHub CLI (if installed)

```bash
gh auth login
# Follow the prompts to authenticate
```

## Testing Your SSH Connection

After adding the key, test it:

```bash
ssh -T git@github.com
```

Expected output:
```
Hi [your-username]! You've successfully authenticated, but GitHub does not provide shell access.
```

## Using SSH with Git

Once your SSH key is added, you can clone repositories using SSH:

```bash
# Instead of HTTPS:
git clone https://github.com/username/repo.git

# Use SSH:
git clone git@github.com:username/repo.git
```

## If You Need to Generate a New Key

If you need to create a new SSH key:

```bash
# Generate a new ED25519 key (recommended)
ssh-keygen -t ed25519 -C "your_email@example.com"

# Or if ED25519 is not supported, use RSA:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Then follow the steps above to add it to GitHub.

## Troubleshooting

### Permission denied error?
- Make sure your key is added to GitHub
- Check SSH agent: `ssh-add -l`
- Add key to agent: `ssh-add ~/.ssh/id_ed25519`

### Multiple keys?
If you have multiple SSH keys, configure them in `~/.ssh/config`:

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

## Your Current SSH Keys

You have these keys in `~/.ssh/`:
- `id_ed25519` (main key)
- `id_ed255aryan_personal` (personal key)

Make sure to add the public key (`.pub` file) to GitHub, not the private key!

