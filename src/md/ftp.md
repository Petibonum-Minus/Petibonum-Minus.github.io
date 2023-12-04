# FTP
## Connection anonymous

```bash=
──(petibonum㉿kali)-[~/Pentest/TryhackMe/Startup]
└─$ ftp 10.10.24.241
Connected to 10.10.24.241.
220 (vsFTPd 3.0.3)
Name (10.10.24.241:petibonum): anonymous
331 Please specify the password.
Password: anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```
## Commandes

    bye or close or quit : Terminates an FTP connection.

    cd : Changes the current working directory on the FTP host server.

    cwd	: Changes the current directory to the specified remote directory.

    dir	: Requests a directory of files uploaded or available for download.

    get	: Downloads a single file.

    ls : Requests a list of file names uploaded or available for download.

    mget : Interactively downloads multiple files.

    mput : Interactively uploads multiple files.

    open : Starts an FTP connection.

    pasv : Tells the server to enter passive mode, in which the server waits for the client to establish a connection rather than attempting to connect to a port the client specifies.

    put	: Uploads a single file.

    pwd	: Queries the current working directory.

    ren	: Renames or moves a file.

    site : Executes a site-specific command.

    type : Sets the file transfer mode: ASCII / Binary

Source : [FTP commands](https://www.ibm.com/docs/en/scbn?topic=SSRJDU/gateway_services/ftp_globalec/SCN_Summary_of_FTP_Client_Commands_b.html)
## Connexion :
    ```bash=
    ftp <ip>
    <username>
    <password>
    ````

## Télécharger depuis le server vers la machine :

```bash=
curl -u <user>:<password> -T <file> ftp://<ip>/
``` 

Source : [FTP upload](https://blog.desdelinux.net/en/send-ftp-file-command-only/)

## Télécharger depuis la machine vers le serveur

    Se placer sur le serveur ftp : 
    ```bash=
    put <file>
    ```
    OK

