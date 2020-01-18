# Disclaimer
**Use at your own risk.** I compiled this for usage in a personal project where it worked fine.

# awslambda-pycrypto
## python2.6 version
* Available in the python2 folder
* [Python Cryptography Toolkit (pycrypto)](https://github.com/dlitz/pycrypto) compiled and packaged for AWS Lambda. Because that is a pain to do.

## python3.7 version
* Available in the python3 folder
* Since support for python2 is ending at the end of 2020 and pycrypto is no longer supported, this version uses:
  * `Python 3.7.4`
  * `pip 9.0.3 from /usr/lib/python3.7/site-packages (python 3.7)`
  * Amazon Linux 2 `Linux 4.14.158-129.185.amzn2.x86_64 #1 SMP Tue Dec 24 03:15:32 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux`
  * [pycryptodome](https://github.com/Legrandin/pycryptodome)

# Setup
Simply download and include the correct Crypto folder in your project, zip and upload it to Lambda.

# Lambda Example:
Directory structure:
```
* myproject
  - Crypto/
  - lambda_handler.py
```
`lambda_handler.py`:
```python
from __future__ import print_function

from Crypto.Hash import SHA256


def lambda_handler(event, context):
    hash = SHA256.new()
    hash.update('message')
    digest = hash.digest()
    print(len(digest))
    print(repr(digest))
    return
```

Log output:
```
START RequestId: 17e0f272-9b91-11e6-bf2d-f756ae83795f Version: $LATEST
32
'\xabS\n\x13\xe4Y\x14\x98+y\xf9\xb7\xe3\xfb\xa9\x94\xcf\xd1\xf3\xfb"\xf7\x1c\xea\x1a\xfb\xf0+F\x0cm\x1d'
END RequestId: 17e0f272-9b91-11e6-bf2d-f756ae83795f
REPORT RequestId: 17e0f272-9b91-11e6-bf2d-f756ae83795f	Duration: 0.28 ms	Billed Duration: 100 ms 	Memory Size: 128 MB	Max Memory Used: 14 MB
```
