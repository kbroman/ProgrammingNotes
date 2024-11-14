## Yubikey


### Ubuntu

<https://support.yubico.com/hc/en-us/articles/360016649099-Ubuntu-Linux-Login-Guide-U2F>

- installation

  ```
  sudo apt install libpam-u2f
  ```

- associate keys

  ```
  mkdir -p ~/.config/Yubico
  pamu2fcfg > ~/.config/Yubico/u2f_keys
  ```

  If more keys, repeat last line with `>>`

- set up sudo

  edit `/etc/pam.d/sudo` to include line `auth [tab] required [tab] pam_u2f.so`
  immediately after the line with `@include common-auth`

- set up login

  edit `/etc/pam.d/gdm-password` (or `/etc/pam.d/lightdm` if using
  `lightdm` rather than `gdm`) similar to sudo case above

- set up tty

  Edit `/etc/pam.d/login` as above



### Duo MFA at UW-Madison

- Go to <https://mfa.wisc.edu>

- Click "Manage MFA Preferences and Devices" (*not* Registern USB
  Security Key)

- Click "Add a device" and then "Security key"

- Seems to work with [Security Key C
  NFC](https://www.yubico.com/product/security-key-series/security-key-c-nfc-by-yubico-black/)
  (that is, you **don't** need the [YubiKey 5C NFC](https://www.yubico.com/product/yubikey-5c-nfc/))
