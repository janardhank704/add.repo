# add.repo
This script can be run through add.repo.
#!/bin/bash

# STEP 1: Set a valid URL for the .repo file
REPO_URL="http://192.168.149.133/add_repo/local_env.repo"

# STEP 2: Set the filename you want to save it as
REPO_NAME="local_env.repo"

# STEP 3: Set the destination directory
DEST_DIR="/etc/yum.repos.d"

# STEP 4: Check for root permission
if [ "$(id -u)" -ne 0 ]; then
    echo "This script must be run as root. Use sudo."
    exit 1
fi

# STEP 5: Download the file using curl
echo "Downloading from $REPO_URL..."
curl -o "$DEST_DIR/$REPO_NAME" "$REPO_URL"

# STEP 6: Check if the download succeeded
if [ $? -eq 0 ]; then
    echo "Repo file downloaded successfully to $DEST_DIR/$REPO_NAME"
else
    echo "Download failed."
    exit 2
fi
