# torrelay

Tor relay with docker / docker compose

> [!IMPORTANT]
>## wollomatic/torrelay is moving to Codeberg
> The new location is https://codeberg.org/wollomatic/torrelay
> 
> The GitHub repo will be archived soon.

## Prerequisities

* You need docker / docker compose installed on a linux machine with amd64 architecture.
* You should know what tor and tor relays are.
* You should know what You are doing.

## Getting Started

The container image is available on docker hub: [https://hub.docker.com/r/wollomatic/torrelay](https://hub.docker.com/r/wollomatic/torrelay/)

**Get the sample configuration from the [Github Repo](https://github.com/wollomatic/torrelay/tree/main/deployment)**

#### configure torrc

* Copy torrc.EXAMPLE to torrc
* Change Nickname and ContactInfo
* If running multiple relays, uncomment MyFamily line and insert relay info
* Check and adjust ORPort, BandwidthRate, MaxAdvertisedBandwidth, MaxMemInQueues
* (Or use your own torrc)

#### configure compose.yaml

* Check and adjust compose.yaml
* run ``docker compose up -d && docker compose logs -f`` to start the relay and check the logs 

## Volumes

* `/etc/tor/torrc` - torrc
* `/var/lib/tor` - tor data directory

## GitHub repository
* [GitHub](https://github.com/wollomatic/torrelay)

## Authors

* **W. Ellsaesser** - *Initial work* - [wollomatic](https://github.com/wollomatic)

## License

This project is licensed under the BSD 3-Clause License - see the [LICENSE](https://github.com/wollomatic/torrelay/blob/main/LICENSE) file for details.

## Acknowledgments

* This project is inspired by [docker-obfs4-bridge](https://gitlab.torproject.org/tpo/anti-censorship/docker-obfs4-bridge)
