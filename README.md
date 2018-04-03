# Orvibo HTTP Server

A web interface and API for controlling B25 and S25 wifi sockets.

## Features

### UI

A very simple interface:

![screenshot](misc/screenshot.png)

### API

| Endpoint                | Method | Description
|-------------------------|--------|-----------------------------------------------------------------------------
| `/logs`                 | GET    | Retrieve the most recent 100 logs in reverse order.
| `/sockets`              | GET    | Retrieve a list of sockets.
| `/sockets/:uid`         | GET    | Retrieve the socket identified by the supplied UID (mac address).
| `/sockets/:uid/:state`  | GET    | Change the state of the socket. Valid states include: `on`, `off`, `toggle`.

## Setup

*Note*: you must use the Homemate App to associate each socket with your Wifi network. Once connected to your network you can control each device using this service.

**Step 1 - Redirect homemate traffic to server**

In order to control the Orvibo devices you must intercept the traffic destined for Homemates servers. The easiest way to accomplish this is to hijack DNS for their domain `homemate.orvibo.com` using Dnsmasq. Note that Dnsmasq must be running on your router or gateway. Most custom router firmwares including DD-WRT and Tomato support Dnsmasq. Apply the following configuration: 

```
# Set primary and secondary DNS servers
server=8.8.8.8
server=8.8.4.4

# Override IP for homemate.orvibo.com
address=/homemate.orvibo.com/192.168.0.10
```

**Step 2 - Retrieve the Orvibo key**

Retrieve the Orvibo key using the script provided [here](https://gist.github.com/Grayda/eb48093bcfb96bfeec9c58ea301f2668). This key is needed in the next step.

**Step 3 - Install, configure, and start service**

* Install [NodeJS](https://nodejs.org/en/) 6.X or higher.
* Checkout this [repository](https://github.com/JCotton1123/orvibo-http-server).
* Run `npm install` to install the dependencies.
* Copy the `config.json.sample` to `config.json` and update the file as necessary.
* Run `node index.js` to start the service.

## Acknowledgements

A big thanks to the following individuals for providing help and code:

* [SandySound](https://github.com/sandysound)
* [Grayda](https://github.com/Grayda/)

