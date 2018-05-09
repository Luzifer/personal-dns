# Luzifer / personal-dns

`personal-dns` is a combination of two DNS servers in one container: [CoreDNS](https://coredns.io/) and Bind9.

The purpose is to be fully independent from provider and third-party DNS servers and have a neat list of additional features:

- No DNS query is sent to your providers DNS servers
- You decide which domains are available to you, no third party company
- Container does not log requesting IPs: You're not traced
- On every build a current list of [IANA](https://www.iana.org/domains/root/db) and [OpenNIC](https://wiki.opennic.org/opennic/dot) registered TLDs is loaded together with their authorative nameservers
- The container includes a [blacklist](https://github.com/StevenBlack/hosts) blocking quite a lot of crap

As soon as you build and roll this DNS container and set your system to use it you should notice a lot of ad- and tracking requests to be gone even for example on your Android device where adblockers does not work that well. Also all connected devices can access any domain registered within the OpenNIC TLDs.

## Usage

### Build and run the container

This is quite easy:

```console
$ docker build -t personal-dns .
$ docker run --rm -ti -p 53:53 -p 53:53/udp personal-dns
$ dig +short @<ip of your container> health.server.test
0.0.0.0
```

### Connect your computer to the container

- On **Mac OS** go into the System Preferences, Network, edit your LAN / WiFi connection, enter the IP your container is reachable into DNS settings
- On **Android** I'm using the [DNS Changer](https://play.google.com/store/apps/details?id=com.frostnerd.dnschanger) App