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


curl -vL "https://api.tv/v1/psConfig?platform=ios&partner=cc&environment=prod&multiple=true&VPversion=9.8.1"
```

Save with a file 

```sh
curl -vL [https://5df09.v.fwmrm.net/ad/g/1](https://5df09.v.fwmrm.net/ad/g/1)\?asnw\=384777\&caid\=xtv_discovery.comDSCH4026362800500002-DSCH4026362800500003\&csid\=xtv_discoverychannel_vod_ios_iphone\&flag\=%2Bemcr%2Bexvt%2Bnucr%2Bslcb%2Bamcb%2Bsltp%2Bplay%2Baeti\&metr\=1127\&mode\=on-demand\&nw\=384777\&prof\=384777%3Axtv_TVE_vod_ios\&pvrn\=1828649572\&resp\=json\&ssnw\=384777\&vdty\=exact\&vdur\=5029000\&vip\=73.153.40.242\&vprn\=1579098288\;_fw_app_bundle\=appStoreId\&_fw_app_store_url\=appStore\&_fw_h_user_agent\=Mozilla%2F5.0+%28iPhone%3B+CPU+iPhone+OS+26_3+like+Mac+OS+X%29+AppleWebKit%2F605.1.15+%28KHTML%2C+like+Gecko%29+Mobile%2F15E148\&_fw_is_lat\=0\&_fw_session_id\=03CDEFD7-A7D3-4A49-B793-2096B4E2693C\&_fw_vcid2\=82419200\;\; > ios.xml

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
