# traefik-proxample

Traefik proxy sample

This example uses 5 nginx containers listening on port 80 being exposed behind
the traefik proxy.

To use the example, create a docker-machine with your favorite provider.

1.  `docker-machine create dm0 -d $PROVIDER` (your provider might require additional arguments
    or environment variables)
2.  `docker-machine ls` - note down the ip address and use your registrar or your hosts file to
    point the hosts web1-web2.domain.tld to the ip address
3.  edit the traefik label `traefik.frontend.rule=Host:` on the services in the docker-compose.yml file
4.  point your local docker cli context to the create docker-machine: `eval $(docker-machine env dm0)`
5.  boot your new reverse proxied services: `docker-compose up -d`
    - check the visualization at web1.domain.tld:8080
    - scale one service: `docker-compose scale web1=3`
    - check the visualization again
6.  visit web1.domain.tld and web1.domain.tld:8080 in your browser
7.  bonus: add automatic letsencrypt certificates to each service by digging deeper
