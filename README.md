shadowsocks-heroku
==================

shadowsocks-heroku is a lightweight tunnel proxy which can help you get through firewalls. It is a port of [shadowsocks](https://github.com/clowwindy/shadowsocks), but through a different protocol.

shadowsocks-heroku uses WebSocket instead of raw sockets, so it can be deployed on [Heroku](https://www.heroku.com/).

Notice that the protocol is INCOMPATIBLE with the origin shadowsocks.

Heroku
------

In my case, my Heroku application name is `david-shadowsocks`. You should replace it with yours.

### Setup

Install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

```
# MacOS
$ brew install heroku/brew/heroku
```

Clone this repository and add a remote. (First you should create a remote application on Heroku).

```
$ git clone https://github.com/daviddwlee84/shadowsocks-heroku.git
$ cd shadowsocks-heroku
$ heroku git:remote -a david-shadowsocks
```

### Usage

```
$ heroku create
```

Push the code (deploy) to Heroku.

```
$ git push heroku master
```

Set a few configs:

```
$ heroku config:set METHOD=rc4-md5 KEY=foobar
```

Install project dependencies with `npm install`:

```
$ npm install
```

Then run:

```
$ node local.js -s david-shadowsocks.herokuapp.com -l 1080 -m rc4-md5 -k foobar -r 80
```

Change proxy settings of your browser into:

```
SOCKS5 127.0.0.1:1080
```

### Troubleshooting

If there is something wrong, you can check the logs by:

```
$ heroku logs -t --app david-shadowsocks
```

Supported Ciphers
-----------------

- rc4
- rc4-md5
- table
- bf-cfb
- des-cfb
- rc2-cfb
- idea-cfb
- seed-cfb
- cast5-cfb
- aes-128-cfb
- aes-192-cfb
- aes-256-cfb
- camellia-256-cfb
- camellia-192-cfb
- camellia-128-cfb
