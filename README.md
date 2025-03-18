Generate key:

```
rm -rf /tmp/s5 ; mkdir /tmp/s5 ; chmod 700 /tmp/s5
echo "batch" >/tmp/s5/gpg.conf
echo "pinentry-mode loopback" >>/tmp/s5/gpg.conf
gpg --full-generate-key --homedir /tmp/s5 --passphrase ''
gpg --list-keys --with-keygrip --homedir /tmp/s5
gpg --homedir /tmp/s5 --armor --export-secret-keys jafo00+uvrepo@gmail.com >uvrepo-private.gpg
gpg --homedir /tmp/s5 --armor --export jafo00+uvrepo@gmail.com >uvrepo-public.asc
gpg --homedir /tmp/s5 --export jafo00+uvrepo@gmail.com >uvrepo-public.gpg
```

Use uvrepo-public.gpg for the line in apt sources:

```
deb [signed-by=/usr/share/keyrings/uvrepo.gpg] https://linsomniac.github.io/uvrepo nobel main
```
