# Tools
## curl
`curl`
- `-H "host: test.com"` add header, for testing vhosts\
- `--insecure` ignore certificate issues

## ssh
`ssh`
- `-R 1337:192.168.1.1:3389` Create listening port on the server forwarding to IP:3389\
- `-L 1337:192.168.1.1:3389` Create listening prot lon the local client forwarding to IP:3389

## SWAKS
Swiss Army Knife for SMTP\
- `--to mail@mail.com` Send to address
- `--server` Server to use
