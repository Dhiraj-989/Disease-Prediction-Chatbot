✨ SageMaker + GitHub Repository Setup Guide

This document explains how to clone this repository inside AWS SageMaker, configure SSH authentication, and push notebook updates back to GitHub without entering passwords or tokens.

🧰 1. Clone This Repository in SageMaker

Open a terminal inside SageMaker and run:

git clone https://github.com/Dhiraj-989/Disease-Prediction-Chatbot.git

cd Disease-Prediction-Chatbot


(Optional) Set Git identity:

git config --global user.name "Dhiraj Kumar"

git config --global user.email "your_email@example.com"

🔐 2. Configure SSH Authentication (Recommended)

SSH lets SageMaker push to GitHub without passwords/tokens.

2.1 Generate SSH key on SageMaker:
ssh-keygen -t ed25519 -C "your_email@example.com"


Press Enter for the file path

Press Enter twice for an empty passphrase

2.2 View the public key:
cat ~/.ssh/id_ed25519.pub

2.3 Add this key to GitHub:

GitHub → Settings → SSH and GPG Keys → New SSH Key
Paste the key and save.

2.4 Switch the repo remote from HTTPS → SSH:
git remote set-url origin git@github.com:Dhiraj-989/Disease-Prediction-Chatbot.git

2.5 First push will ask:
Are you sure you want to continue connecting (yes/no)? yes


After that, SSH works permanently.

📁 3. Notebook Storage in SageMaker

SageMaker stores notebooks under:

/home/ec2-user/SageMaker/


But the GitHub repo exists at:

/home/ec2-user/Disease-Prediction-Chatbot


If a notebook is created in SageMaker, move it into the Git repo:

mv /home/ec2-user/SageMaker/<folder>/Model.ipynb \
   /home/ec2-user/Disease-Prediction-Chatbot/


(Replace file or folder names as needed.)

🚀 4. Pushing Notebook Changes to GitHub

Always work inside the real Git repo:

cd /home/ec2-user/Disease-Prediction-Chatbot


Then stage, commit, and push:

git add .

git commit -m "Update notebook"

git push


Because SSH is configured:

No username required

No password required

No personal access token required

🛠 5. Useful Commands
Find where a notebook is saved:
find ~ -name "Model.ipynb"

Check current Git remote:
git remote -v

Remove wrong or duplicated repo folders:
rm -rf <folder-name>
