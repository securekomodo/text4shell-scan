# Frequently Asked Questions

## The Read operation timed out
```
[•] Initiating DNS callback server (interact.sh).
Traceback (most recent call last):
  <- truncated ->
  File "/opt/homebrew/lib/python3.10/site-packages/urllib3/connectionpool.py", line 449, in _make_request
    six.raise_from(e, None)
  <- truncated ->
TimeoutError: The read operation timed out

During handling of the above exception, another exception occurred:
```
I have found that interact.sh has been a bit unreliable as of late. There are options in the tool to use a different OOB provider. Try using a custom DNS callback host 


## DNS callback error

```
Traceback (most recent call last):
File "/Users/user/src/Text4Shell-scan/text4shell-scan.py", line 362, in
main()
File "/Users/user/src/Text4Shell-scan/text4shell-scan.py", line 332, in main
dns_callback = Interactsh()
File "/Users/darkcode/src/Text4Shell-scan/text4shell-scan.py", line 195, in init
self.register()
File "/Users/user/src/Text4Shell-scan/text4shell-scan.py", line 206, in register
raise Exception("Can not initiate interact.sh DNS callback client")
Exception: Can not initiate interact.sh DNS callback client
```

It means that the DNS callback provider is down, it's blocked on your network, or you can not connect to the DNS callback provider due to networking issues. You can use an different DNS Callback provider (eg.. with `--dns-callback-provider dnslog.cn`), or you can use a custom DNS callback host with ` --custom-dns-callback-host`.

---

## Running with Python 2

```
File "text4shell-scan.py", line 136
fuzzing_headers["Referer"] = f'https://{fuzzing_headers["Referer"]}'
```

It should be related to Python 2 compatibility. The tool requires a modern version of Python 3.

---

# Dependencies issue

```
from Crypto.Cipher import AES, PKCS1_OAEP
ModuleNotFoundError: No module named 'Crypto'
```

This should be related to Pycrypto. Please install the latest Python PyCryptodome version.
