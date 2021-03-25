# wkhtmltopdf heroku Buildpack

This is a [Heroku buildpack][0] for bundling a compatible [wkhtmltopdf][1]
binary with your environment.

NOTE: Heroku-18 or Heroku-20 refer to the Ubuntu version under the hood (i.e., Ubuntu 18 or 20)

IMPORTANT: Ubuntu is a fork of Debian, so Debian packages can be installed on Ubuntu -- so download the debian version of wkhtmltoX. The "bionic" (and maybe "focal") versions are for Ubuntu. The others (Buster, Bullseye) are for pure Debian.

IMPORTANT: To determine Heroku machines architecture, run "heroku run bash" (invoking heroku cli there) and then run "dpkg --print-architecture". If you use "uname -m" it will tell you "x86_64" but if you run "dpkg --print-architecture" it will likely say "amd64". Use this information to choose the appropriate package to download from the wkhtmltopdf site. x86_64 is name of specific 64-bit Instruction Set Architecture. This instruction set was released in 1999 by AMD (Advanced Micro Devices). AMD later rebranded it to amd64. Other 64-bit Instruction Set Architectures different from x86_64 is IA-64 (released by Intel in 1999).

CUSTOM FONTS: Basically, include a link directly in the HTML you want to pdf: https://stackoverflow.com/questions/41295382/custom-fonts-not-working-in-generated-pdf-using-wkhtmltopdf-library  you can also put font files directly in the "fonts" dir in this repo and the compile script will install them.

## Versions

* Buildpack:   `0.1`
* wkhtmltopdf: `wkhtmltox-0.12.6-1.amazonlinux2.x86_64.rpm` by default

## Usage

[Add this buildpack][2] to your Heroku application to install the `wkhtmltopdf`
and `wkhtmltoimage` binaries, and the corresponding library `libwkhtmltox`,
into the dynos:

```bash
$ heroku buildpacks:add https://github.com/jqsjqs/wkhtmltopdf-heroku-buildpack --index 1
```

If you want to use a `wkhtmltopdf` version other than the default set
`WKHTMLTOPDF_DOWNLOAD_URL`:

```bash
heroku config:set WKHTMLTOPDF_DOWNLOAD_URL="https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb"
```



You can see all the releases here:
https://github.com/wkhtmltopdf/packaging/releases/

### Clearing Repo Cache

Remember to clean your repository cache if you are updating the version of
buildpack. To do that, run:

```bash
$ heroku plugins:install https://github.com/heroku/heroku-repo.git
$ heroku repo:purge_cache -a appname
```


### Credits

Most of this code was from the [chap/wkhtmltopdf-heroku-18-buildpack](https://github.com/chap/wkhtmltopdf-heroku-18-buildpack)

[0]: http://devcenter.heroku.com/articles/buildpacks
[1]: http://wkhtmltopdf.org/
[2]: https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app
