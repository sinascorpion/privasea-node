***Privanetix Node Setup guide***

**Requirements** 👇 

  ▫️ OS: Debian/Ubuntu (Recommended) 
  
  ▫️ Storage: 100GB available 
  
  ▫️ Memory: 8GB RAM 
  
  ▫️ Processor: 16 cores, x86 architecture Network:
  
  ▫️ Public static IP 
  
  ▫️ Port: Open TCP port 8181 


1. *Install Docker* (skip this if Docker is already installed).
```bash
command -v docker >/dev/null || (echo "Installing Docker..." && apt-get install -y ca-certificates curl gnupg lsb-release && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io) && command -v docker-compose >/dev/null || (echo "Installing Docker Compose..." && curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose.tmp && [[ -f /usr/local/bin/docker-compose ]] && rm /usr/local/bin/docker-compose && mv /usr/local/bin/docker-compose.tmp /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose)
```

2. Pull the latest Privanetix Node image using the following command:
```bash
docker pull privasea/acceleration-node-beta:latest
```

3. **Create a Directory:**
```bash
mkdir -p ~/privasea/config && cd ~/privasea
```

4. **Generate Node Address and Save It:**
Enter your password to create a keystore and save the node address:
```bash
docker run --rm -it -v "$HOME/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore
```

Then move the keystore file:
```bash
mv $HOME/privasea/config/UTC--* $HOME/privasea/config/wallet_keystore
```

5. **Set Up the Node on the Platform:**

  ▫️Go to: https://deepsea-beta.privasea.ai/privanetixNode

  ▫️Connect your testnet wallet.

  ▫️Assign a name to your node.

  ▫️Set the commission rate (e.g., 1%).

  ▫️Enter the node address you generated earlier.

  ▫️Click the "Set up my node" button.

6. **Set Up the Node on VPS:**
Back in your VPS, run the following command to start the node:
```bash
KEYSTORE_PASSWORD=ENTER_YOUR_KEYSTORE_PASSWORD && docker run -d --name privanetix-node -v "$HOME/privasea/config:/app/config" -e KEYSTORE_PASSWORD=$KEYSTORE_PASSWORD privasea/acceleration-node-beta:latest
```
Replace ENTER_YOUR_KEYSTORE_PASSWORD with the password you created in step 4.

7. **Claim Faucet and Stake:**
Follow the instructions starting from step 4 in the guide here:
https://www.privasea.ai/privanetix-node

