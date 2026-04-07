# Wazuh Lab Setup

## 1. Setting up the wazuh dashboard.
Due to low system specifications i decided to do my wazuh lab in docker. I set up my docker by:

1. Cloning the Wazuh Docker repository to my system:
```bash
git clone https://github.com/wazuh/wazuh-docker.git -b v4.14.4
```

2. Navigating to single-node directory.
```bash
cd wazuh-docker/single-node/
```

3. Generating wazuh certificates
```bash
docker compose -f generate-indexer-certs.yml run --rm generator
```

## 1. Setting up endpoint.
I this lab set up i decided to set up Ubuntu Server 24.04.4 LTS. Running it inside another system. After the installation I set the IP to static. The IP address is 192.168.25.17. After that wazuh agent was installed on that server using the following commands.
