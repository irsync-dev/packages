# irsync package repository

The signed apt and dnf repositories for [irsync](https://irsync.org),
served by GitHub Pages at [dist.irsync.org](https://dist.irsync.org).
Packages contain both `irsync` and `fileset`, for x86_64 and arm64.
Stable releases only.

## Install

Debian, Ubuntu:

```sh
sudo install -d /etc/apt/keyrings
sudo curl -fsSL https://dist.irsync.org/irsync.gpg -o /etc/apt/keyrings/irsync.gpg
echo "deb [signed-by=/etc/apt/keyrings/irsync.gpg] https://dist.irsync.org/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/irsync.list
sudo apt update
sudo apt install irsync
```

Fedora, RHEL:

```sh
sudo curl -fsSL https://dist.irsync.org/irsync.repo -o /etc/yum.repos.d/irsync.repo
sudo dnf install irsync
```

The signing key is [irsync.asc](https://dist.irsync.org/irsync.asc), owned
by `irsync releases <releases@irsync.org>`.

## About this repo

Everything here except this README is written by the release workflow in
[irsync-dev/irsync](https://github.com/irsync-dev/irsync) (see
`packaging/update-repo.sh` there). Don't edit it by hand: the next release
overwrites it. Change the page and repo files in `packaging/repo/` in the
main repo instead.

The repo keeps the three newest versions. Older releases are on the
[GitHub Releases page](https://github.com/irsync-dev/irsync/releases).

Layout:

- `apt/`: the Debian repo (suite `stable`, component `main`), signed
  `InRelease` and `Release.gpg`.
- `rpm/x86_64/`, `rpm/aarch64/`: the rpm repos. Each package and each
  `repomd.xml` is signed.
- `irsync.asc`, `irsync.gpg`: the public signing key, armored and binary.
- `irsync.repo`: the dnf repo file.
- `index.html`, `CNAME`: the Pages site at dist.irsync.org.
