# Easy-as-Py Cryptography (AKA crypter)

A Python package for performing complex Cryptographic functions with simple function calls. The crypter package follows the best practices from Google's Python Style Guide (to the best of my abilities). Functions signatures are typed and docstrings should be sufficienly explanatory. 

## requirements

The crypter package wraps pycryptodome. To install the requirements:

`pip install pycryptodome`

To use the PKI scripts for generating public key infrastructure you will also need OpenSSL, which is probably installed on your box by default.

## Installation & Setup

1) Download: `git clone https://github.com/0x00wolf/easyaspy-cryptography`
2) `cd easyaspy-cryptography`
3) Create a venv: `python -m venv venv; source ./venv/bin/activate`
4) Install pycryptodome: `pip install pycryptodome`
5) Pop a Python shell and learn about the package: `python; import crypter; crypter.{tab complete}; help(crypter.rsa.key.interactive_keypair)`

## Example Usage:

The following example will peform the following steps. It will import the sender's RSA private key, and the receiver's RSA pubic key, sign a message with a local RSA private key, generate a 256-bit session key, use a ChaCha20-Poly1305 AEAD stream-cipher to encrypt the message with the session key, wrap the session key with the receiver's RSA public, and return the wrapped key, signature, and ciphertext.

```python
message = "I am a message that's about to get encrypted"
senders_private_key, receivers_public_key = crypter.rsa.key.load_keys(private_pem='./privkey.pem, public_pem='./pubkey.pem')
wrapped_key, signature, ciphertext = crypter.encrypt.signed_message(
  encoded_string=message.encode(),
  private_key=senders_private_key,
  public_key=receivers_public_key)
```


## Error Handling:

The crypter package will catch all low level errors and reraise a CrypterError with an appropriate error message. To handle CrypterError's decide what should happen to the execution flow at a high level.

`from crypter.CrypterError import CrypterError`

