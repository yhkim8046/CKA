Q: Where is the configuration file located for configuring the CoreDNS service?
A: $ kubectl -n kube-system describe deployments.apps coredns | grep -A2 Args | grep Corefile