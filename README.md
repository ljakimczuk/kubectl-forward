# The Kubectl Socat-based Forward plugin

The kubectl-forward plugin sets up an in-cluster TCP proxy for relaying traffic to a given service running outside the cluster.

## Getting Started

These instructions will get you a copy of this plugin up and running.

### Installing

To install the plugin, execute the following command:

```
sudo curl -L https://github.com/ljakimczuk/kubectl-forward/raw/master/bin/kubectl-forward -o /usr/local/bin/kubectl-forward
sudo chmod a+x /usr/local/bin/kubectl-forward
```

### Usage

In order to route the traffic to the service through the cluster, pass the service address and destination port to the plugin. Optionally you are allowed to specify the source port as well, see the help output below.

```
Usage:
  forward [-n namespace] host [sport:]dport

Examples:
  # Forward TCP traffic to the RDS host from your local 5432 port.
  kubectl forward backend.123456789012.eu-west-1.rds.amazonaws.com 5432

  # Forward TCP  traffic the the Redis host from your local 6379 port.
  kubectl forward redis.123456789012.euw1.cache.amazonaws.com 6379

  # Forward TCP traffic to the RDS host from your local 50000 port.
  kubectl forward backend.123456789012.eu-west-1.rds.amazonaws.com 50000:5432

  # Forward TCP  traffic the the Redis host from your local 50000 port.
  kubectl forward redis.123456789012.euw1.cache.amazonaws.com 50000:6379
```

#### AWS RDS example

In order to forward traffic to the RDS backend use:

```
$ kubectl forward backend.123456789012.eu-west-1.rds.amazonaws.com 5432
Forwarding from 127.0.0.1:5432 -> 5432
Forwarding from [::1]:5432 -> 5432
```

Then use the `localhost` as you would do in a regular port-forwarding case, for example:

```
$ psql -h localhost -U postgresql -d postgres
Password for user postgresql:
```

#### AWS Redis example

In order to forward traffic to the Redis service use:

```
$ kubectl forward redis.123456789012.euw1.cache.amazonaws.com 6379
Forwarding from 127.0.0.1:6379 -> 6379
Forwarding from [::1]:6379 -> 6379
```

Then use the `localhost` as you would do in a regular port-forwarding case, for example:

```
$ redis-cli -h localhost -p 6379 --tls
localhost:6379>
```
