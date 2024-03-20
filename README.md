# shotput: shell otp utopia

A portable shell script to generate TOTPs from the command line.

## Example Usage
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

$ ./shotput example
enter aes-256-cbc decryption password:
358094

$ ./shotput example reveal
enter aes-256-cbc decryption password:
GEZDGNBVGY3TQOJQGEZDGNBVGY3TQOJQ
SHA512
60
```
