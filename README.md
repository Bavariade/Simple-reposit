#/usr/bin/env bash
# create_simple_repo.sh
# Usage: ./create_simple_repo.sh
set -e

REPO_NAME="simple-repo"
DESCRIPTION="A basic repository for code and project management."
AUTHOR="Your Name <you@example.com>"

mkdir -p "$REPO_NAME"
cd "$REPO_NAME"

# Initialize git
git ini

# README.md
cat > README.md <<EOF
# $REPO_NAME

$DESCRIPTION

## Contents
- \`main.py\`: example entrypoint
- \`LICENSE\`: MIT License
- \`.gitignore\`: common ignores

## Usage
Run the example:
\`\`\`bash
python main.py
\`\`\`
EOF

# Example main.py
cat > main.py <<'PY'
#!/usr/bin/env python3
"""
simple-repo: example entrypoint
"""
def main():
    print("Hello from simple-repo!")

if __name__ == "__main__":
    main()
PY
chmod +x main.py

# .gitignore (Python)
cat > .gitignore <<EOF
__pycache__/
*.pyc
.env
venv/
env/
.DS_Store
EOF

# LICENSE (MIT)
cat > LICENSE <<'EOF'
MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
...
EOF

# Initial commit
git add .
git commit -m "chore: initialize simple-repo with README, example, and license"

# Optional: create GitHub repo (requires GitHub CLI 'gh' and authentication)
if command -v gh >/dev/null 2>&1; then
  gh repo create "$REPO_NAME" --public --description "$DESCRIPTION" --source=. --remote=origin --push
else
  echo "Note: 'gh' not found. Create a remote repo manually and push:"
  echo "  git remote add origin git@github.com:USERNAME/$REPO_NAME.git"
  echo "  git branch -M main"
  echo "  git push -u origin main"
fi
