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
heroku: Press any key to open up the browser to login or q to exit:
Logging in... done
set git remote heroku to https://git.heroku.com/david-shadowsocks.git
```

### Usage

Push the code (deploy) to Heroku.

```
$ git push heroku master
```

Set a few configs:

```
$ heroku config:set METHOD=rc4-md5 KEY=yourPassword
Setting METHOD, KEY and restarting ⬢ david-shadowsocks... done, v4
KEY:    yourPassword
METHOD: rc4-md5
```

Install project dependencies with `npm install` or `yarn install`:

```
$ npm install
```

Then run:

```
$ node local.js -s david-shadowsocks.herokuapp.com -l 1080 -m rc4-md5 -k yourPassword -r 80
server listening at { address: '127.0.0.1', family: 'IPv4', port: 1080 }
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

* [Heroku - Troubleshooting Node.js Deploys](https://devcenter.heroku.com/articles/troubleshooting-node-deploys#check-your-buildpack)
* [Heroku Node.js Support](https://devcenter.heroku.com/articles/nodejs-support)
    * Specifying a Node.js Version

        You should always specify a Node.js version that matches the runtime you’re developing and testing with

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
