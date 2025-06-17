# Curl

Pretty lightweight tool to quickly get network requests and responses from the server.

## command builder

[curl CLI request builder](https://curlbuilder.com/)

## Download file FTP

```sh
curl -L -R -O ftp_full_server_file_address
```


You can open ftp://ftp.gnu.org/ in Firefox and Chrome without going to the Finder, which is what Safari does.

If you have a complete URL to download, use curl, as in

```sh
curl -L -R -O ftp://ftp.gnu.org/gnu/bc/bc-1.07.1.tar.gz
```

Do man curl or curl --help for more information.
[SO ](https://apple.stackexchange.com/questions/320781/missing-ftp-command-line-tool-on-macos)


## GET

```bash
curl https://www.example.com/
```

Another example

```sh
curl -s "http://url.something.com/filepath/filename-.m3u8?sz=asfa"
```
## Source

man help - curl
[Manual](https://curl.se/docs/manual.html)

```sh
man curl
```

[SO | curl D param](https://stackoverflow.com/questions/46673210/curl-d-parameter)


### Allowlist

Check if ur whitelisted / allowlist for IP address blocked.

```sh
curl -4 -Lvs https://domain.mainDomain.us/TESTTESTTEST
curl -6 -Lvs https://domain.mainDomain.us/TESTTESTTEST
```


## Cheatsheet

[quickref.me  | curl](https://quickref.me/curl.html)

[devhints.io | curl](https://devhints.io/curl)

## Error 

### SSL error

[SO | curl-60-ssl-certificate-problem-unable-to-get-local-issuer-certificate](https://stackoverflow.com/questions/24611640/curl-60-ssl-certificate-problem-unable-to-get-local-issuer-certificate)
