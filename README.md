## Malicious Docker Payloads

This docker image is intended to emulate malicious behavior to test [EDR/Anti](https://www.wicar.org/test-malware.html) Virus solutions on Docker/Kubernetes [Hosts/Clusters](https://www.wicar.org/test-malware.html).

## How To Run
```
git clone https://github.com/pxcs/Payloads_Docker && cd Payloads_Docker
docker build -t Payloads_Docker:latest .
docker run Payloads_Docker:latest
```

## What Tests are Running?

### Anti Virus
[EICAR Malware Sample](https://www.wicar.org/test-malware.html)

### Network Endpoint Protection
[Flightsim Malicious Network Sample](https://github.com/alphasoc/flightsim)
