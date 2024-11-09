
# Microsoft Graph PowerShell Mail Module
I wrote this module to make interacting with MSGraph mail APIS easier.

## Available Functions

### 2. `Get-MGMailFolderFromPath`
Allows you to get a mailfolder like you would file paths using your userid as the root "directory"

**Parameters:**
- `-Path`: Mail folder path, e.g., `"user@domain.com\Inbox\My Folder"`.
- `-ShowChildren`: List child folders if present for better visibility 

**Example:**
```powershell
Get-MGMailFolderFromPath -Path "user@domain.com\Sent Items"
```

### 1. `Get-MailFolderMessages`
You can pipe the output of `Get-MGMailFolderFromPath` into this to get messages inside that folder.
The function will save a golbal machine variable named after the Folder ID with a date the last time you checked the folder
allowign you to do quick delta checks for new messages. You can have this skipped with the `-NoSetTime` parameter.

**Parameters:**
- `-Id`: The folder ID.
- `-UserID`: User email or ID.
- `-New`: Only retrieve new messages since the last check.
- `-Silent`: Suppress output.
- `-NoSetTime`: Skip setting the last check time.

**Example:**
```powershell
Get-MGMailFolderFromPath -Path "user@domain.com\Inbox" | Get-MailFolderMessages 
```

### 3. `Send-GraphMailMessage`
Sends an email message with optional attachments.

**Parameters:**
- `-Subject`: Email subject.
- `-Body`: Message body.
- `-From`: Sender’s email address.
- `-To`: Array of recipient email addresses.
- `-Attachments`: File paths for attachments.
- `-BodyAsHTML`: Use HTML formatting for the body.

**Example:**
```powershell
# Send an email with an attachment
$toAddresses = @("recipient@domain.com")
$attachments = @("C:\path\to\file.txt")
Send-GraphMailMessage -Subject "Test Email" -Body "Hello, this is a test." -To $toAddresses -Attachments $attachments
```

## Usage Notes
Ensure to connect to Microsoft Graph using `Connect-MgGraph` before using these functions to authenticate your session. This module simplifies email interactions, making it suitable for automated notifications, folder management, and message retrieval directly from PowerShell.
