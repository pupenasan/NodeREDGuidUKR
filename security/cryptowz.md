# crypto-wz 1.0.2

https://flows.nodered.org/node/crypto-wz

Node-RED nodes using CryptoJS to encrypt and decrypt messages

​             `npm install crypto-wz`                    

Node-RED nodes using CryptoJS to encrypt and decrypt messages

# CryptoJS

JavaScript library of crypto standards.

Supported algorithms:   

Encrypt and Decrypt Nodes:

- crypto-js/aes
- crypto-js/des
- crypto-js/RC4
- crypto-js/Rabbit
- crypto-js/TripleDES

Digest Node

- crypto-js/md5
- crypto-js/sha1
- crypto-js/sha3
- crypto-js/sha224
- crypto-js/sha256
- crypto-js/sha384
- crypto-js/sha512

HMAC (Hash-based Message Authentication Code) Node

- crypto-js/hmac-md5
- crypto-js/hmac-sha1
- crypto-js/hmac-sha3
- crypto-js/hmac-sha224
- crypto-js/hmac-sha256
- crypto-js/hmac-sha384
- crypto-js/hmac-sha512

Encode and Decode

- crypto-js/enc-base64
- crypto-js/enc-Hex
- crypto-js/enc-Latin1
- crypto-js/enc-utf8
- crypto-js/enc-Utf16
- crypto-js/enc-Utf16BE
- crypto-js/enc-Utf16LE

# Запит на нові алгоритми

Не соромтеся відкривати випуск для нових алгоритмів, але майте на увазі, що це `crypto-js` Node-RED bridge, тому будуть реалізовані лише алгоритми, які підтримуються структурою реалізації.