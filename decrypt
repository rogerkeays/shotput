#!/bin/sh
#
# Decrypt text line by line. This is useful for storing secrets such as
# passwords or TOTP keys in your journal. Use <ctrl-c> to stop this script, or
# <ctrl-z> to fork it to the background. By forking to the background, you
# won't need to reenter your encryption password to restart the script. Just
# run `fg`.
#

alias decrypt="openssl enc -aes-256-cbc -pbkdf2 -base64 -A -pass env:PASS -in /dev/stdin -d"

stty -echo
read -p "Enter your decryption password: " PASS
export PASS
stty echo
echo

while [ 1 ]; do
  echo -n "< "
  read LINE
  [ "$LINE" ] && echo "$LINE" | decrypt
done

