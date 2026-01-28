# GitLab SSL Configuration (Self-Signed Certificate)
Before configuring SSL, when accessing GitLab via

![image](/uplodes/gitlab-interface.png)

## 1. Create the SSL directory
GitLab expects SSL certificates in /etc/gitlab/ssl.

```
sudo mkdir -p /etc/gitlab/ssl
sudo chmod 700 /etc/gitlab/ssl
```
This ensures only root can access the certificate files.

## 2. Generate a self-signed certificate

Run the following command:
```
sudo openssl req -newkey rsa:2048 -nodes -keyout gitlab.local.key \
-x509 -days 365 -out gitlab.local.crt
```

During the prompt
Common Name (CN) must be:
`gitlab.local`
This must match the GitLab URL.

## 3. Secure the certificate files
Set correct permissions so GitLab can read them safely.
```
sudo chmod 600 /etc/gitlab/ssl/gitlab.local.key
sudo chmod 644 /etc/gitlab/ssl/gitlab.local.crt
```

## 4. Configure GitLab to use HTTPS

Open GitLab configuration file /etc/gitlab/gitlab.rb and set the external URL:

` external_url "https://gitlab.local"`

Configure the SSL certificate paths:
```
nginx['ssl_certificate']     = "/etc/gitlab/ssl/gitlab.local.crt"
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/gitlab.local.key"
```
Save and exit.

## 5. Apply the configuration
Run:
`sudo gitlab-ctl reconfigure`


Dans ton navigateur, sur `https://gitlab.local`

The GitLab SSL certificate is a self-signed certificate issued for gitlab.local, valid from 07 January 2026 to 07 January 2027

![image](/uplodes/cert.png)
