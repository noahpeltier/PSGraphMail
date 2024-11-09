
# Microsoft Graph PowerShell Mail Module
This PowerShell module interacts with the Microsoft Graph API to manage email. With this module, users can retrieve emails, navigate through mail folders, and send messages directly from PowerShell. It is designed to streamline common email tasks for system administrators.

## Available Functions

### 1. `Get-MailFolderMessages`
Fetches messages from a specified mail folder.

**Parameters:**
- `-Id`: The folder ID.
- `-UserID`: User email or ID.
- `-New`: Only retrieve new messages since the last check.
- `-Silent`: Suppress output.
- `-NoSetTime`: Skip setting the last check time.

**Example:**
```powershell
# Retrieve all messages from the "Inbox" folder of a specific user
$inboxFolder = Get-MGMailFolderFromPath -Path "user@domain.com\Inbox"
Get-MailFolderMessages -Id $inboxFolder.Id -UserID $inboxFolder.UserID
```

### 2. `Get-MGMailFolderFromPath`
Locates a user's mail folder by a specified path.

**Parameters:**
- `-Path`: Mail folder path, e.g., `"user@domain.com\Inbox"`.
- `-ShowChildren`: List child folders if present.

**Example:**
```powershell
# Retrieve a reference to the "Sent Items" folder
$sentFolder = Get-MGMailFolderFromPath -Path "user@domain.com\Sent Items"
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
