# py-filetracker
Image tracker/data management utility.

Managing a huge amount of images and keeping track of everything is painful

This tools tries to resolve a tracking problem when images are split between two folders:
1. A first folder who contains all the collected images
2. Another folder who contains only a subset of selected images

It will check the content of those two folders and build a diff list to keep track of images that are stored and images that are selected for further use.

The results are written into a Google Spreadsheet file.

## Disclaimer
This tool was developped for a specific usecase. It uses a harcoded regex to collect the informations about the files. It might be necessery to dive into the code (`src/track.py`) to adapt it to other scenarios.

## Google Configuration
### 1. Create a Google account

### 2. Create a Google Cloud Project
1. Access the [Google Cloud Console](https://console.cloud.google.com/).
2. Open the menu (☰) -> IAM and Admin -> Create a Project. Or press `ctrl + O` and click New project.
3. Create a project.
4. Select the created project.

### 3. Activate the Google Sheet API
1. Open the Google Cloud Console menu (☰) -> APIs & Services -> Library
2. Search for **Google Sheet API**
3. Press **Enable**

### 4. Create a Service Account
1. Open the Google Cloud Console menu (☰) -> IAM and Admin -> Service Accounts
2. Press on **+ Create Service Account**
3. Create an account with the name you want
4. Press **Done**
5. Copy the account email for later.

### 5. Generate auth keys
1. Open the Google Cloud Console menu (☰) -> IAM and Admin -> Service Accounts
2. Click on the previously created account
3. Access the **Keys** menu
4. Press **Add key** -> **Create new key**
5. Select JSON and press **Create**
6. A JSON file is download.
7. Copy this file into the `account` folder of this repo.
8. Rename the file to `service-account.json`

### 6. Google Sheet configuration
1. Create an empty Google Sheet
2. Copy the spreadsheet ID
3. Provide access to the spreadsheet for the service account with the **Share** button. Two possible ways:
    1. Share the file with everyone who has the link. Set the role to Editor
    
    OR

    2. Add the service account email to the list of users with access. Give this user the Editor role.

## Installation
After setting up a Google API service account, follow the next steps

1. Clone this repo

2. Create a Python virtual environnment: `python -m venv .venv`

3. Activate the virtual environnment: `. .venv/bin/active`

4. Install the dependencies: `pip install -r requirements.txt`

5. Copy the `.env.example` file to `.env`

6. Set the environnment variables:

    - `ALL_IMAGES_FOLDER`: The base folder where all the images are stored
    - `SELECTED_IMAGES_FOLDER`: The folder with the selected images are.

    The difference between the files will be done through those two folders.

    - `SPREADSHEET_ID`: The Google Spreadsheet ID.
    - `SHEET_NAME`: The name of the sheet where the to copy the informations to.

7. Execute the tool: `python src/track.py`

## Run the script as a periodical services
Instead of running the script manually it is possible to configure it as a periodic service. To do so, use something such as crontab to periodically execute the script.