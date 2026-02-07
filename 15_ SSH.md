# Add SSH remote origin:
    git remote add origin git@github.com:username/repo.git


# Verify connection:
    git remote -v


# Set default branch (optional):
    git branch -M main
    git push -u origin main


# Generate SSH key:
    ssh-keygen -t ed25519 -C "your_email@example.com"


# Add to SSH agent:
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519


# Copy public key:
    cat ~/.ssh/id_ed25519.pub


# Confirm if successful:
    ssh -T git@github.com


# Change remote URL from HTTPS to SSH:
    git remote set-url origin git@github.com:pravinmishraaws/Pravin-Mishra-Portfolio-Template.git


# Now push:
    git push -u origin feature/footer-v1


# Use personal access token (PAT) as password:
  1. Create PAT on GitHub: Settings → Developer settings → Personal access tokens → Tokens (classic)
  2. Select repo permissions


# Configure credential helper:
    git config --global credential.helper store


# Try push again (enter username and PAT as password):
  git push -u origin feature/footer-v1
  git remote remove origin
  git remote add origin git@github.com:Ralphlarry/Pravin-Mishra-Portfolio-Template.git
