<h1 align="center">text4shell-scan</h1>
<h4 align="center">A fully automated, accurate, and extensive scanner for finding vulnerable text4shell hosts</h4>

<img width="1441" alt="image" src="https://user-images.githubusercontent.com/4809643/196782122-d7c9d6fc-dec3-4de4-81bc-c495381dcd33.png">

# Features

- Support for lists of URLs.
- Fuzzing for more than 60 HTTP request headers.
- Fuzzing for HTTP POST Data parameters.
- Fuzzing for JSON data parameters.
- Supports DNS callback for vulnerability discovery and validation.
- WAF Bypass payloads.

---
# Description

We have been researching the Text4SHell RCE (CVE-2022-42889) since it was released. We are open-sourcing an open detection and scanning tool for discovering and fuzzing for Text4Shell RCE CVE-2022-42889 based off Fullhunts log4j project back in 2021 (MAJOR CREDIT TO THEM). This shall be used by security teams to scan their infrastructure for Text4Shell RCE, and also test for WAF bypasses that can result in achieving code execution on the organization's environment.

It supports DNS OOB callbacks out of the box, there is no need to set up a DNS callback server.

https://nvd.nist.gov/vuln/detail/CVE-2022-42889


# Usage

```python
$ python3 text4shell-scan.py -h
[•] CVE-2022-42889 - Apache Commons Text RCE Scanner
[•] Scanner provided by @securekomodo

usage: text4shell-scan.py [-h] [-u URL] [-p PROXY] [-l USEDLIST] [--request-type REQUEST_TYPE] [--headers-file HEADERS_FILE] [--run-all-tests] [--exclude-user-agent-fuzzing]
                     [--wait-time WAIT_TIME] [--waf-bypass] [--custom-waf-bypass-payload CUSTOM_WAF_BYPASS_PAYLOAD]
                     [--dns-callback-provider DNS_CALLBACK_PROVIDER] [--custom-dns-callback-host CUSTOM_DNS_CALLBACK_HOST] [--disable-http-redirects]

optional arguments:
  -h, --help            show this help message and exit
  -u URL, --url URL     Check a single URL.
  -p PROXY, --proxy PROXY
                        send requests through proxy
  -l USEDLIST, --list USEDLIST
                        Check a list of URLs.
  --request-type REQUEST_TYPE
                        Request Type: (get, post) - [Default: get].
  --headers-file HEADERS_FILE
                        Headers fuzzing list - [default: headers.txt].
  --run-all-tests       Run all available tests on each URL.
  --exclude-user-agent-fuzzing
                        Exclude User-Agent header from fuzzing - useful to bypass weak checks on User-Agents.
  --wait-time WAIT_TIME
                        Wait time after all URLs are processed (in seconds) - [Default: 5].
  --waf-bypass          Extend scans with WAF bypass payloads.
  --custom-waf-bypass-payload CUSTOM_WAF_BYPASS_PAYLOAD
                        Test with custom WAF bypass payload.
  --dns-callback-provider DNS_CALLBACK_PROVIDER
                        DNS Callback provider (Options: dnslog.cn, interact.sh) - [Default: interact.sh].
  --custom-dns-callback-host CUSTOM_DNS_CALLBACK_HOST
                        Custom DNS Callback Host.
  --disable-http-redirects
                        Disable HTTP redirects. Note: HTTP redirects are useful as it allows the payloads to have a higher chance of reaching vulnerable systems.
```

## Scan a Single URL

```shell
$ python3 text4shell.py -u https://<enter URL here>
```

## Scan a Single URL using all Request Methods: GET, POST (url-encoded form), POST (JSON body)


```shell
$ python3 text4shell.py -u https://<enter URL here> --run-all-tests
```

## Discover WAF bypasses against the environment.

```shell
$ python3 text4shell.py -u https://<enter URL here> --waf-bypass
```

## Scan a list of URLs

```shell
$ python3 text4shell.py -l urls.txt
```

# Installation

```
$ pip3 install -r requirements.txt
```

# Docker Support

```shell
git clone [https://github.com/fullhunt/log4j-scan](https://github.com/CyberRedline/Text4Shell-Scan).git
cd Text4Shell-Scan
sudo docker build -t Text4Shell-Scan .
sudo docker run -it --rm Text4Shell-Scan

# With URL list "urls.txt" in current directory
docker run -it --rm -v $PWD:/data Text4Shell-Scan -l /data/urls.txt
```


# Legal Disclaimer
This project is made for educational and ethical testing purposes only. Usage of Text4Shell-Scan for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program.


# License
The project is licensed under MIT License.


# Author
*Bryan Smith*
* Twitter: [https://twitter.com/securekomodo](https://twitter.com/securekomodo)
