# Pi-Hole-DoH-DNS-over-HTTPS-Docker - Cloudflare
## Official latest Pi-hole docker image with DoH (DNS over HTTPS) powered by Cloudflare - Docker

I have build this docker image using the amd64 architecture.

Testing your configuration

To test your configuration, after proper configured the new DNS adress in your router or computer, go to the following:page: 

https://1.1.1.1/help
https://https://www.cloudflare.com/en-gb/ssl/encrypted-sni/

You should note the line "Using DNS over HTTPS (DoH)" flagged as Yes.

#
Docker-compose example:

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    image: indomitus/pihole-doh:latest
    # Pi-hole doesn't currently support running as non-root
    # https://github.com/pi-hole/docker-pi-hole/issues/685
    # user: "1000:1000"
    restart: always
    ports:
      - 53:53
      - 53:53/udp
      - 67:67/udp
      - 82:80/tcp
    volumes:
      - ~/pihole/data/pihole:/etc/pihole/
      - ~/pihole/data/dnsmasq:/etc/dnsmasq.d/
    cap_add:
      - NET_ADMIN
    environment:
      - TZ=Europe/Rome
      - WEBPASSWORD=<password>
      - PIHOLE_DNS_=127.0.0.1#5053
  
