# Atomic Desktops with the LTS kernel
These are tests to create images that use the official Linux longterm release kernel. It gets released every year and is supported for 2 years.

Using it should guarantee more stability and less worries, but might also create unknown bugs!

## Installation

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase --reboot ostree-unverified-registry:ghcr.io/fantastic-fedora/IMAGE-NAME:latest
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase --reboot ostree-image-signed:docker://ghcr.io/fantastic-fedora/IMAGE-NAME:latest
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

Available images:

- kinoite-lts
- silverblue-lts

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/blue-build/template
```
