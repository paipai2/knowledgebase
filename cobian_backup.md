# CobianBackup
Install &amp; Configure Cobian Backup on local windows

## 1. Download Cobian Backup from this link
https://files.cobiansoft.com/programs/cbSetup.exe

## 2. Install On your PC
- Accept The conditions
- Choose your installation path (Default: “C:\Program Files (x86)\Cobian Backup 11”)
- Select Application (no auto-start) & Next 

## 3. Create Backup Task
- When creating a task, we need to configure some parameter in
- General (Task Name)
- Files (Source & Destination)
- Schedule (Schedule type, Timer)
- Archive (Compression Type)

## 4. Add a new task
- Name this task whatever you like.
- Select Full in Backup Type. 

## 5. Adding local directory to backup
- Connect to sftp in notepad++.
- Download a file and right click the file name, select “Full File Path to Clipboard”.
- Paste it to somewhere & it will show something like this:
- **C:\Users\User\AppData\Roaming\Notepad++\plugins\Config\NppFTP\Cache\FTPUSER@1.2.3.4\home\FTPUSER\PATH\FOLDER**
- Copy the file path before the sftp name. For example, my sftp downloaded file stored in
- **C:\Users\User\AppData\Roaming\Notepad++\plugins\Config\NppFTP\Cache**
- Add the path name into Cobian Backup
- Click on “Add” button and choose manual. It will prompt Up a new window, key in the path and click “OK”.
- Same for destination. Click “Add” button and key in your backup path manually or select “Directory” to choose your backup folder. 

##  6. Setting up schedule to run backups.
After adding the Backup Source and Destination, move to the “Schedule” page and set when you want to run the backup. 
For example, I will set it to run backup every minute.
- Select “Timer” in Schedule Type, and set minutes to 1. 

## 7. Auto clean backups
Next, we will set how many backups you want to keep in “Dynamics” page. For example, I will store only 5 backups. 
- When running the backup, it will delete all the backups created earlier and keep 5 latest backups.
- Set the amount base on your needs, disk space, file size & etc. 

## 8. Compress your backup files
- Move to the “Archive” Page and select “Compression type” if you want to compress the backup files to save your disk space. 
- Change “Archive Comment” to rename the backup files name.
- **This is optional, you can do this base on your needs, disk space & etc.** 
- If you don’t want to compress it, just select “No Compression” will do. 
- Finally, click “OK” to save the backup task and click run to start your backup.

## To backup separately, create a task & add the ftp name behind the path in Step 5.
Example:
- C:\Users\User\AppData\Roaming\Notepad++\plugins\Config\NppFTP\Cache\stu2018dy0331@192.168.1.214\
