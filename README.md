# Проблема  
Из-за блокировки российских адресов на <https://releases.hashicorp.com> стало невозможно устанавливать любимые инструменты через [Homebrew](https://brew.sh)  
Этот репозиторий создан чтобы решить эту проблему  

# Быстрый старт  

```
$ brew tap vandud/hashicorp-tap
$ brew install vandud/hashicorp-tap/terraform
$ brew install vandud/hashicorp-tap/vault
```

# Как работает  
Эта репа - форк [hashicorp/homebrew-tap](https://github.com/hashicorp/homebrew-tap) в котором просто заменены ссылки на бинари с releases.hashicorp.com на зеркало от YCloud - <https://hashicorp-releases.yandexcloud.net/>  
Ниже лог установки в котором это хорошо видно  
```
$ brew search terraform
==> Formulae
iam-policy-json-to-terraform                    terraform-graph-beautifier                      terraform-ls                                    terraform-rover                                 vandud/hashicorp-tap/consul-terraform-sync
terraform                                       terraform-inventory                             terraform-lsp                                   terraform_landscape                             vandud/hashicorp-tap/terraform
terraform-docs                                  terraform-local                                 terraform-provider-libvirt                      terraformer                                     vandud/hashicorp-tap/terraform-ls

If you meant "terraform" specifically:
It was migrated from homebrew/cask to homebrew/core.
$ brew install vandud/hashicorp-tap/terraform
==> Auto-updating Homebrew...
==> Fetching vandud/hashicorp-tap/terraform
==> Downloading https://hashicorp-releases.yandexcloud.net/terraform/1.9.8/terraform_1.9.8_darwin_arm64.zip
Already downloaded: /Users/vandud/Library/Caches/Homebrew/downloads/b4e7c359ef1dde3c5df8894625c7f6d6e989c4af2ddbfac4e2a454b52e8188c2--terraform_1.9.8_darwin_arm64.zip
==> Installing terraform from vandud/hashicorp-tap
🍺  /Users/vandud/homebrew/Cellar/terraform/1.9.8: 5 files, 83.9MB, built in 1 second
==> Running `brew cleanup terraform`...
```

# Команда для замены ссылок  
```
rg releases.hashicorp.com -l Formula/ | xargs -I% sed -i '' 's/releases.hashicorp.com/hashicorp-releases.yandexcloud.net/g' %
```

---

[![Heimdall](https://heimdall.hashicorp.services/api/v1/assets/homebrew-tap/badge.svg?key=f0ea6d408d7a7798bcd4f6ef4a40fe9c791109ca85d2f20d5630a9f4abafa9f6)](https://heimdall.hashicorp.services/site/assets/homebrew-tap)

# HashiCorp Homebrew Tap

## What is Homebrew?

Package manager for macOS (or Linux), see more at https://brew.sh

## What is a Tap?

A third-party (in relation to Homebrew) repository providing installable
packages (formulae) on macOS and Linux.

See more at https://docs.brew.sh/Taps

## How do I install packages from here?

```sh
brew install hashicorp/tap/name
```

You can also only add the tap which makes formulae within it
available in search results (`brew search` output):

```sh
brew tap hashicorp/tap
```

Note: to clone the tap via SSH you will need to use:

```sh
brew tap hashicorp/tap https://github.com/hashicorp/homebrew-tap
```

While you may search across taps, it is necessary to always use
fully qualified name (incl. the `hashicorp/tap/` prefix)
when refering to formulae in external taps such as this one
outside of search.

## What packages are available?

With the following commands, you can install the latest generally available (GA) version of each product:
```sh
# Formulae
brew install hashicorp/tap/athena-cli
brew install hashicorp/tap/boundary
brew install hashicorp/tap/consul
brew install hashicorp/tap/consul-dataplane
brew install hashicorp/tap/consul-enterprise
brew install hashicorp/tap/consul-template
brew install hashicorp/tap/consul-terraform-sync
brew install hashicorp/tap/hc-install
brew install hashicorp/tap/hcdiag
brew install hashicorp/tap/hcp
brew install hashicorp/tap/levant
brew install hashicorp/tap/nomad
brew install hashicorp/tap/nomad-enterprise
brew install hashicorp/tap/nomad-pack
brew install hashicorp/tap/packer
brew install hashicorp/tap/sentinel
brew install hashicorp/tap/terraform
brew install hashicorp/tap/terraform-ls
brew install hashicorp/tap/tf-migrate
brew install hashicorp/tap/tfstacks
brew install hashicorp/tap/vault
brew install hashicorp/tap/vault-enterprise
brew install hashicorp/tap/vault-radar
brew install hashicorp/tap/waypoint

# Casks
brew install hashicorp/tap/hashicorp-boundary-desktop
brew install hashicorp/tap/hashicorp-vagrant
```

Prereleases (including as alpha's, beta's, and release candidates) will not be available in this tap.

## Why should I install packages from this tap?

Formulae for the same HashiCorp software may exist in other taps
or the [community-maintained main tap](https://github.com/Homebrew/homebrew-core).
This may raise a question of why would someone prefer one tap over the other.

The _community-maintained tap_ compiles HashiCorp software on Homebrew's own infrastructure, and builds it according to the local formulae definition.

Formulae _in this tap_ are maintained by HashiCorp, which means that it distributes
the exact (byte-to-byte) same binaries which are published to https://releases.hashicorp.com

 - macOS binaries are signed by HashiCorp and the signature can be verified
	per instructions on the [HashiCorp's Security](https://www.hashicorp.com/security#code-signature-verification) page
 - Teams maintaining HashiCorp software choose Go version and any build flags _deliberately_ while
 	factoring in support, security and other concerns. Binaries distributed through this tap reflect this.
 - Updating of formulae is automated, which means that updates become available as they're released.

### Why doesn't HashiCorp maintain formulae in the `homebrew-core` (main tap)?

Homebrew's core team prefers to keep `homebrew-core` as community maintained and built from source to maintain consistency across vendors in terms of expectations around contents and updates. See [relevant discussion](https://discourse.brew.sh/t/maintenance-of-formulas-by-vendor/7649) for more information.

## Contributing

Check out our [contribution guidelines for this project](./CONTRIBUTING.md)
