# shotput: shell otp utopia

A portable shell script to generate TOTPs from the command line.

## Usage

    shotput service [reveal]

Generates an OTP for the given service. If the service is not found, you will
be prompted to provide a new secret key and an encryption password. New
secrets are added to the config file in `$HOME/.config/shotput.keys`. Each
secret is encrypted seperately and may use a different password.

If `reveal` is specified, the secret key for the given service will be
displayed, rather than generating an OTP.

## Examples

Add a new TOTP secret:
```
$ ./shotput example
Enter a new base32 secret key for example:GEZDGNBVGY3TQOJQGEZDGNBVGY3TQOJQ
Enter TOTP algorithm (default SHA1):SHA512
Enter TOTP timeout (default 30s):60
enter aes-256-cbc encryption password:
Verifying - enter aes-256-cbc encryption password:
Encrypted secret key for example and added to /home/username/.config/shotput.keys

enter aes-256-cbc decryption password:
166313
```

Check your secrets are encrypted:
```
$ cat ~/.config/shotput.keys
example="U2FsdGVkX19jANPjexyaiXOsTgZvdwKyWfDm4yWGh9rZ3G1iqfd5RyNX/hyGKmJOeeZYPF7FKrfD/dgRswb72Q== SHA512 60"
```

Generate an OTP:
```
$ ./shotput example
enter aes-256-cbc decryption password:
358094
```

Recover your secret key:
```
$ ./shotput example reveal
enter aes-256-cbc decryption password:
GEZDGNBVGY3TQOJQGEZDGNBVGY3TQOJQ
SHA512
60
```

## Installation

shotput requires `oathtool >=2.6.6` and `openssl`:

    sudo apt install oathtool openssl

Place the `shotput` script on your path:

    cd $HOME/bin
    wget https://raw.githubusercontent.com/rogerkeays/shotput/main/shotput

Or clone with github:

    git clone https://github.com/rogerkeays/shotput.git

## Extracting Secret Keys From QR Codes

`zbarimg` can be used to decode QR codes. Save the QR code as an image file, and run:

    sudo apt install zbar-tools
    zbarimg $file

This should produce an `otpauth://` URL which contains your secret key, and TOTP parameters.

## Legacy Systems (Debian 10)

`shotput` can be made to work with older versions of `oathtool` that do not read from stdin. Replace `oathtool -` with `oathtool $(cat /dev/stdin)`. This is not recommended on multi-user systems, because the plain text secret key will be visible to `ps` and other tools while `oathtool` is running.

## Related Resources

  * [otpclient](https://https://github.com/paolostivanin/OTPClient): another linux OTP utility which includes a command line tool
  * [otpauth](https://github.com/dim13/otpauth/): a tool which can convert Google Authenticator links to standard oauth secret keys
  * [How to use TOTP with Google accounts](https://webapps.stackexchange.com/questions/127464/enabling-2fa-on-a-google-account-how-to-get-totp-secret): hidden settings, because Google is "not a conventional company".
  * [How to extract TOTP secrets from the MyGov app](https://gist.github.com/hacker1024/5d0845863e2dced27fd5eebc4ac95a39): for Australians who are over installing government apps.
  * [python-vipacess](https://github.com/dlenski/python-vipaccess): a tool to provision secrets for Symantec VIP Access without installing any apps.
  * [More stuff you never knew you wanted](https://rogerkeays.com).

