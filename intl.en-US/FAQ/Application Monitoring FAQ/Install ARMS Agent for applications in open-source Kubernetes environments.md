# Install ARMS Agent for applications in open-source Kubernetes environments {#concept_106851_zh .concept}

This topic lists FAQ about installing ARMS Agent for applications in open-source Kubernetes environments, and provides solutions.

## Why does my application not start? {#section_sfb_dsy_pgb .section}

Run the following command to view the arms-pilot-system logs and troubleshoot the problem according to the logs:

```
kubectl logs -f {arms-pilot-arms-pilot-XXX} -n arms-pilot-system
```

## How can I view the logs of ARMS Agent? {#section_lnd_hsy_pgb .section}

On the worker of the Kubernetes cluster, view the logs in /home/admin/.opt/ArmsAgent/logs/xxxx.log.

