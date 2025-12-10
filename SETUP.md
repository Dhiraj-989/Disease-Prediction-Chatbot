✨ SageMaker + GitHub Repository Setup Guide

This document explains how to clone this repository inside AWS SageMaker Notebook Instance, configure SSH authentication, and save notebooks so that updates sync cleanly to GitHub.

🧰 1. Clone This Repository Inside SageMaker Folder

Always clone into the ~/SageMaker/ directory, since this is where SageMaker Notebook Instances store all notebooks.

Open a terminal:

cd ~/SageMaker

git clone https://github.com/Dhiraj-989/Disease-Prediction-Chatbot.git

cd Disease-Prediction-Chatbot


Configure Git (first time only):

git config --global user.name "Dhiraj Kumar"

git config --global user.email "your_email@example.com"

🔐 2. Configure SSH Authentication (No Passwords Needed)

2.1 Generate SSH key:

ssh-keygen -t ed25519 -C "your_email@example.com"


Press Enter for file path

Press Enter twice for empty passphrase

2.2 View your public key:
cat ~/.ssh/id_ed25519.pub

2.3 Add key to GitHub:

GitHub → Settings → SSH and GPG Keys → New SSH Key
Paste the key → Save

2.4 Switch remote URL to SSH:
git remote set-url origin git@github.com:Dhiraj-989/Disease-Prediction-Chatbot.git


Verify:

git remote -v

📁 3. Notebook Storage in SageMaker

SageMaker Notebook Instances automatically save notebooks inside:

~/SageMaker/


So your repo must stay inside this folder:

/home/ec2-user/SageMaker/Disease-Prediction-Chatbot


If a notebook appears in .virtual_documents, ignore it — always open the notebook from the repo folder above.

🚀 4. Workflow: Edit Notebooks & Push Changes

Open JupyterLab → navigate to:

~/SageMaker/Disease-Prediction-Chatbot/Model.ipynb


After editing:

cd ~/SageMaker/Disease-Prediction-Chatbot

git add .

git commit -m "Update notebook"

git push


SSH → No username/password/token required.

🛠 5. Useful Commands
Find a notebook file:
find ~ -name "Model.ipynb"

Check which repo is real:
find ~ -type d -name ".git"

Remove accidental duplicate directories:
rm -rf ~/SageMaker/.virtual_documents/Disease-Prediction-Chatbot
rm -rf ~/Disease-Prediction-Chatbot   # only if duplicated
