# Install Weblate

Weblate is an open-source web-based translation tool with version control integration. It provides propagation of translations across components, quality checks and automatic linking to source files. For more information see https://weblate.org. The documentation is here https://docs.weblate.org/en/latest.

## Create a DNS A record for your (sub) domain that points to your server

Create a new `A record` on the server that is called `weblate.example.com` that points to the public IP of the virtual server.

## Gmail as Weblate Email Host

With the Gmail SMTP server, you'll be able to send emails from your Gmail account using other email clients, such as Outlook or Thunderbird. But more importantly, you can also use Gmail's SMTP server to send emails. Gmail let's you send up to 500 emails per day, which is more than enough for the most small weblate projects.

### How to Find the SMTP Server for Gmail

- Gmail SMTP server address: smtp.gmail.com
- Gmail SMTP name: Your full name
- Gmail SMTP username: Your full Gmail address (e.g. you@gmail.com)
- Gmail SMTP password: The password that you use to log in to Gmail
- Gmail SMTP port (TLS): 587
- Gmail SMTP port (SSL): 465

### The Gmail SMTP Server Still Work With Two-Factor Authentication

You can use the SMTP server if you have enabled two-factor authentication on your Google account. You will need to generate an app password so that the app can still connect. You can generate an app password by https://myaccount.google.com/apppasswords. This page while logged into your Google account.

## Add an SSH key to your GitLab account

- Sign in in Weblab
- Go to Administration -SSH-key's
- Copy the Public Ed25519 SSH key
- Sign in to GitLab
- On the left sidebar, select your avatar
- Select Edit profile
- On the left sidebar, select SSH key's
- Select Add new key
- Paste the Public Ed25519 SSH key

## Add a Webhook in your Repository

Add this line with your domain for a new Webhook.

```bash
https://weblate.example.com/hooks/gitlab/
```

## Deploy Weblate in Portainer

If Portainer is used for Weblate, a `docker-compose.yaml` and a `stack.env` file is required.

docker-compose.yaml

```bash
version: '3.8'
services:
  weblate:
    ports:
    - 8080:8080
    image: weblate/weblate
    tmpfs:
    - /run
    - /tmp
    volumes:
    - weblate-data:/app/data
    - weblate-cache:/app/cache
    env_file:
    - stack.env
    restart: always
    read_only: true
    depends_on:
    - database
    - cache
  database:
    image: postgres:15-alpine
    env_file:
    - stack.env
    volumes:
    - postgres-data:/var/lib/postgresql/data
    restart: always
  cache:
    image: redis:7-alpine
    restart: always
    read_only: true
    command: [redis-server, --save, '60', '1']
    volumes:
    - redis-data:/data
volumes:
  weblate-cache: {}
  weblate-data: {}
  postgres-data: {}
  redis-data: {}
```
.env or stack.env

```
# See Weblate documentation for detailed description:
# https://docs.weblate.org/en/latest/admin/install/docker.html#generic-settings

# Weblate setup
WEBLATE_DEBUG=0
WEBLATE_LOGLEVEL=WARNING
WEBLATE_SITE_TITLE=Weblate
WEBLATE_SITE_DOMAIN=weblate.example.com
WEBLATE_ADMIN_NAME=user.name@gmail.com
WEBLATE_ADMIN_EMAIL=user.name@gmail.com
WEBLATE_ADMIN_PASSWORD=geheim
WEBLATE_SERVER_EMAIL=user.name@gmail.com
WEBLATE_DEFAULT_FROM_EMAIL=user.name@gmail.com
WEBLATE_ALLOWED_HOSTS=*
WEBLATE_REGISTRATION_OPEN=0

# Extra
WEBLATE_TIME_ZONE=Europe/Berlin
#WEBLATE_MT_GOOGLE_KEY=
#WEBLATE_MT_GOOGLE_CREDENTIALS=
#WEBLATE_MT_GOOGLE_PROJECT=
#WEBLATE_MT_GOOGLE_LOCATION=
#WEBLATE_SOCIAL_AUTH_GITHUB_KEY=
#WEBLATE_SOCIAL_AUTH_GITHUB_SECRET=
#WEBLATE_SOCIAL_AUTH_BITBUCKET_KEY=
#WEBLATE_SOCIAL_AUTH_BITBUCKET_SECRET=
#WEBLATE_SOCIAL_AUTH_FACEBOOK_KEY=
#WEBLATE_SOCIAL_AUTH_FACEBOOK_SECRET=
#WEBLATE_SOCIAL_AUTH_GOOGLE_OAUTH2_KEY=
#WEBLATE_SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET=

#WEBLATE_OFFLOAD_INDEXING=1
#WEBLATE_GOOGLE_ANALYTICS_ID=
WEBLATE_ENABLE_HTTPS=1
#WEBLATE_IP_PROXY_HEADER=HTTP_X_FORWARDED_FOR
WEBLATE_REQUIRE_LOGIN=1

# Secure Host settings
SECURE_HSTS_SECONDS=1
SECURE_SSL_REDIRECT=1
SESSION_COOKIE_SECURE=1

# LDAP Auth
#WEBLATE_AUTH_LDAP_SERVER_URI=ldap://ldap.example.org
#WEBLATE_AUTH_LDAP_USER_DN_TEMPLATE=uid=%(user)s,ou=People,dc=example,dc=net
#WEBLATE_AUTH_LDAP_USER_ATTR_MAP=first_name:name,email:mail

# PostgreSQL setup
POSTGRES_PASSWORD=weblate
POSTGRES_USER=weblate
POSTGRES_DATABASE=weblate
POSTGRES_HOST=database
POSTGRES_PORT=

# Cache setup
# https://docs.weblate.org/en/latest/admin/install.html#production-cache
REDIS_HOST=cache
REDIS_PORT=6379

# Mail server, the server has to listen on port 587 and understand TLS
WEBLATE_EMAIL_HOST=smtp.gmail.com
WEBLATE_EMAIL_USE_TLS=1
WEBLATE_EMAIL_USE_SSL=0
# Do NOT use quotes here
WEBLATE_EMAIL_HOST_USER=user.name@gmail.com
# Do NOT use quotes here
WEBLATE_EMAIL_HOST_PASSWORD=hvoljhkxqqmtbets
CLIENT_MAX_BODY_SIZE=200M
```