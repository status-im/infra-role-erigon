# Description

This role configures a [Erigon](https://github.com/ledgerwatch/erigon) Docker container.

The image used is the official [thorax/erigon](https://hub.docker.com/r/thorax/erigon).

# Configuration

Some important settings are:
```yaml
erigon_network_name: 'mainnet'
erigon_service_name: 'erigon-{{ erigon_network_name }}'
erigon_log_level: 'debug'
```
It is also quite important to enable the right APIs for the right hostnames:
```yaml
erigon_rcp_api: 'eth,net,erigon,admin,engine'
erigon_rpc_extra_vhost: 'erigon.example.org'
```
By default we create a [Consul service definition](https://www.consul.io/docs/agent/services.html):
```yaml
erigon_consul_enabled: true
erigon_consul_extra_tags: ['my-cute-erigon']
```
For the rest see the [`defaults/main.yml`](./defaults/main.yml) config file.

# Management

The container is created and managed with [Docker Compose](https://docs.docker.com/engine/reference/commandline/compose/):
```
admin@erigon-01.aws-eu-central-1a.rocket.prod:/docker/erigon-rocketpool-mainnet % docker-compose ps
          Name                         Command               State                               Ports                            
----------------------------------------------------------------------------------------------------------------------------------
erigon-rocketpool-mainnet   /usr/local/bin/erigon --ch ...   Up      0.0.0.0:30303->30303/tcp, 0.0.0.0:30303->30303/udp,          
                                                                     42069/tcp, 42069/udp, 0.0.0.0:6060->6060/tcp, 8080/tcp,      
                                                                     0.0.0.0:8545->8545/tcp, 8546/tcp, 127.0.0.1:8551->8551/tcp,  
                                                                     9090/tcp
```
