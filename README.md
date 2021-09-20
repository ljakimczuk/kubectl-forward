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

In order to route the traffic to the service through the cluster, pass the service address and port to the plugin, for example:

```
$ kubectl forward database.nonexisting.com 5432
Forwarding from 127.0.0.1:5432 -> 5432
Forwarding from [::1]:5432 -> 5432
```

Then use the `localhost` in order to connect to the service, for example:

```
$ psql -h localhost -U postgresql -d postgres
Password for user postgresql:
```
