Was introduced by Ikwan my colleague. 

Have a look to it [https://rclone.org/downloads/](https://rclone.org/downloads/)  

or use brew [https://formulae.brew.sh/formula/rclone](https://formulae.brew.sh/formula/rclone)  

ChatGPT knows it too, so it is convenient  

```
1. Follow the prompts:

    Select New remote.
    Give it a name (e.g., myserver).
    Choose the type of storage: sftp.
    Enter the required details such as:
        Host (IP or domain of the remote server),
        Username (SSH username),
        Port (default is 22 for SSH),
        Path to the SSH key (if you're using key-based authentication).

Example:

Enter a name for the remote: myserver
Choose a number from below, or type in your own value: sftp
SSH Host: my.remote.server
User: username
SSH Port (leave blank to use default): 22
Path to SSH key file (leave blank to use password): /path/to/ssh/key

Test the connection when prompted.

2. Sync Large Files

To sync large files between your local machine and the remote server, use the following commands:

    Upload files from local to remote:

rclone sync /path/to/local/dir myserver:/path/to/remote/dir

Download files from remote to local:

    rclone sync myserver:/path/to/remote/dir /path/to/local/dir

The sync command ensures that the destination matches the source by deleting any extra files in the destination that are not in the source. If you don’t want this behavior, use copy instead.

```


Resume Interrupted Transfers

Rclone automatically resumes interrupted transfers, making it ideal for large files.
