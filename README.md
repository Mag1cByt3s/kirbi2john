# kirbi2john
Fixed version of https://github.com/nidem/kerberoast/blob/master/kirbi2john.py to make it work with Python3

## Usage

Convert .kirbi ticket into a file john can crack
```bash
python3 ./kirbi2john.py <ticket.kirbi>
```

This will create a file called `crack_file`. We then can modify the file a bit to be able to use Hashcat against the hash.
```bash
sed 's/\$krb5tgs\$\(.*\):\(.*\)/\$krb5tgs\$23\$\*\1\*\$\2/' crack_file > forhashcat.txt
```

We can then run the ticket through Hashcat to recover the passphrase
```bash
hashcat -m 13100 forhashcat.txt /usr/share/wordlists/rockyou.txt
```
