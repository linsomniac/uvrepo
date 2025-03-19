# uv Apt Repository

This package builds an apt repo of the latest "uv" package for
x64 Linux and publishes it to a GitHub Pages.

To use:

```
sudo wget -O /usr/share/keyrings/uvrepo.gpg https://linsomniac.github.io/uvrepo/pubkey.gpg
sudo chmod 644 /usr/share/keyrings/uvrepo.gpg
echo "deb [signed-by=/usr/share/keyrings/uvrepo.gpg] https://linsomniac.github.io/uvrepo any main" | sudo tee /etc/apt/sources.list.d/uvrepo.list
apt update
apt install uv
```

Note, this is a simple package, it simply takes the uv download
tar file of the binaries, and makes a simple deb package containing
the `uv` and `uvx` binaries.

## For Deploying

To deploy your own repo to github pages, you will need to generate
a new key:

```bash
rm -rf repo-key ; mkdir repo-key ; chmod 700 repo-key
echo "batch" >repo-key/gpg.conf
echo "pinentry-mode loopback" >>repo-key/gpg.conf
gpg --full-generate-key --homedir repo-key --passphrase ''
gpg --list-keys --with-keygrip --homedir repo-key
gpg --homedir repo-key --armor --export-secret-keys [EMAIL_ADDR] >private.asc
gpg --homedir repo-key --export [EMAIL_ADDR] >public.gpg
```

The private keyfile `uvrepo-private.asc` needs to be added to your
github project as a secret environment variable called "GPG_PRIVATE_KEY".
You also need to add the key id as a non-secret variable "KEY_ID".

Use uvrepo-public.gpg for the line in apt sources:

```
deb [signed-by=/usr/share/keyrings/uvrepo.gpg] https://linsomniac.github.io/uvrepo nobel main
```
