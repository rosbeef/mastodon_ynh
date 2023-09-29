## Important points to read before installing

- **Mastodon** require a dedicated **root domain**, eg. `domaine.tld` or `mastodon.domain.tld`, with no other apps installed on that domain. You can't change the domain once installed.
- The user choosen during the installation is automatically created in Mastodon with admin rights
- It seems important to close registrations for your Mastodon, so that it remains a private body. We invite you to block remote malicious instances from the administration interface. You can also add text on your home page.

## Using *screen* in case of disconnect

```
$ sudo apt install screen
$ screen
$ sudo yunohost app install https://github.com/YunoHost-Apps/mastodon_ynh.git
```
Recover after disconnect:
```
$ screen -d
$ screen -r
```

#### Using separate domains for Serving and Identity

It is possible to use one domain for serving (like social.example.com) and another for the user identities (like @user@example.com).
In this installation simple set the Local Domain field with the relevant domain.
If the Identity domain is locally managed and properly entered, appropriate redirects will be set up, otherwise you will need to set them up manually.

Example of setting up the required redirect in nginx:
```
{
  server example.com;
  # Other example.com settings...
  ### This is the relevant part:
  location ~ ^/.well-known/(host-meta|nodeinfo|webfinger)/ {
    return 301 https://__DOMAIN__$request_uri;
  }
  ### Until here is the relevant part
}
```

