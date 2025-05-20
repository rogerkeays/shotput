#!/bin/sh
#
# Encrypt text line by line. This is useful for storing secrets such as
# passwords or TOTP keys in your journal. Use <ctrl-c> to stop this script, or
# <ctrl-z> to fork it to the background. By forking to the background, you
# won't need to reenter your encryption password to restart the script. Just
# run `fg`.
#

alias encrypt="openssl enc -aes-256-cbc -pbkdf2 -base64 -A -pass env:PASS -in /dev/stdin"

stty -echo
read -p "Enter your encryption password: " PASS
echo
read -p "Re-enter your encryption password: " PASS2
stty echo
echo

if [ "$PASS" = "$PASS2" ]; then
  export PASS
else
  echo "Sorry, your passwords don't match"
  exit 1
fi

while [ 1 ]; do
  echo -n "> "
  read LINE
  if [ "$LINE" ]; then
    echo "$LINE" | encrypt
    echo
  fi
done

