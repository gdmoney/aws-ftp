# AWS FTP


## Project Overview
Instructions to deploy a managed SFTP server using the **AWS Transfer Family** service.


## Solution Components
- AWS Transfer Family
- Amazon S3
- AWS IAM
- [WinSCP](https://winscp.net/eng/index.php) (Windows S/FTP file transfer client)


## Deployment
### WinSCP
**Create a new key pair**
- Tools > Run PuTTYgen > Type of key: RSA > Generate > Save private key > copy public key


### Amazon S3
**Create a new bucket**
- S3 > Create bucket


### AWS IAM
**Create a new role**
- IAM > Access management > Roles > Create role > Service: Transfer > Policy: AmazonS3FullAccess > Role name: `FTP-ROLE`


### AWS Transfer Family
**Create a new server**
- Create server > Protocol: SFTP > Identity provider: Service managed > Endpoint config: Publicly accessible > Domain: S3

**Create a new user**
- Add user > Username: `<FTP_USERNAME>` > Role: `FTP-ROLE` > Policy: Existing policy > Home directory: `<S3_BUCKET_NAME>` > Restricted = CHECK > SSH public keys: `<PUB_KEY>`


### WinSCP
**Create a new session**
- Protocol: SFTP
- Hostname: `<AWS_FTP_ENDPOINT>`
- Port: 22
- User: `<FTP_USERNAME>`
- Password:
- Advanced > SSH > Authentication > Private key file: `<C:\PATH\TO\PRIVATE_KEY.ppk>`

**Disable timestamp preservation**
- Options > Preferences > Transfer > Default > Edit > Common options > Preserve timestamp = UNCHECK
