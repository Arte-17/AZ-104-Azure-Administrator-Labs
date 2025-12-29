# My Azure Lab - Part 1: Entra ID (Users & Groups)

## What I did
I set up a test user and a group in my Azure tenant using the CLI. The goal was to automate the process so I don't have to click around the portal.

## The Script I used
I ran this in the Azure Cloud Shell (Bash).

```bash
UPN="practice_user@AArte98hotmail.onmicrosoft.com"
GRP="Marketing_Team"

# 1. Create the user
az ad user create --display-name "Practice User" \
                  --password "AzurePass123!" \
                  --user-principal-name "$UPN"

# 2. Create the group 
az ad group create --display-name "$GRP" --mail-nickname "mktteam"

# 3. Add user to group
# I found out it's better to use the Object ID than the email to avoid errors
USER_ID=$(az ad user show --id "$UPN" --query id -o tsv)

az ad group member add --group "$GRP" --member-id "$USER_ID"
