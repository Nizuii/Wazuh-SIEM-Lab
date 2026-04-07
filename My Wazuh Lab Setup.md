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

4. Setting Wazuh Docker deployment using the docker compose command:
```bash
docker compose up -d
```

After the deployment is completed wait for 2 to 3 minutes for the dashboard to load. After that open the browser and enter: `https://localhost` or `https://<private ip address>`.

<img width="1882" height="961" alt="image" src="https://github.com/user-attachments/assets/6b154039-066c-4c54-ab7c-1b3eb6b6fa9d" />

## 1. Setting up endpoint.
I this lab set up i decided to set up Ubuntu Server 24.04.4 LTS. Running it inside another system. After the installation I set the IP to static. The IP address is 192.168.25.17. After that wazuh agent was installed on that server using the following commands.

1. Adding the Wazuh repository and install the agent
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && sudo chmod 644 /usr/share/keyrings/wazuh.gpg

echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list

sudo apt update
sudo apt install wazuh-agent -y
```

2. Pointing the agent at my Wazuh Manager
```bash
sudo WAZUH_MANAGER='192.168.25.7' WAZUH_AGENT_NAME='ubuntu-server-lab' dpkg-reconfigure wazuh-agent
```

3. Starting the agent and enabling it on boot.
```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

4. Checking whether if it runs.
```bash
sudo systemctl status wazuh-agent
```
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/4265e2a5-fe61-4824-8d56-c784b387b261" />
