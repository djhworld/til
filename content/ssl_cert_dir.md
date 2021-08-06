+++
title = "how SSL_CERT_DIR works in golang (on linux systems)"

date = 2021-08-06

[taxonomies]
tags = ["golang"]
+++

_This applies to linux based systems only_

Setting the environment variable `SSL_CERT_DIR` allows you to add some additional certificates to the (go) system cert pool, e.g. self-signed CAs for internal systems.

Note this is in _addition to_ any root CAs that are already in your system level CA certificates files/bundles (see [src/crypto/x509/root_linux.go;l=8-15](https://cs.opensource.google/go/go/+/refs/tags/go1.16.7:src/crypto/x509/root_linux.go;l=8-15) 

Side effect: setting this variable will cause the system to stop scanning the default cert directories [https://cs.opensource.google/go/go/+/refs/tags/go1.16.7:src/crypto/x509/root_linux.go;l=17-23](https://cs.opensource.google/go/go/+/refs/tags/go1.16.7:src/crypto/x509/root_linux.go;l=17-23). 

To mitigate this, you _can_ use colon syntax to make sure all locations you want are scanned.

```
SSL_CERT_DIR=/etc/ssl/certs:/usr/local/ssl/my-custom-certs/
```
