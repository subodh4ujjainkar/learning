# Step by step guide to Docker installation in Ubuntu
1. Update repositories
   > `sudo apt update`

2. Allow `apt` to install packages over HTTPS
   > `sudo apt install ca-certificates curl gnupg`

3. Add Docker gpg key to apt using below commands
    ```
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```
4. Include Docker repository into apt sources list
    ```
    echo \
      "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
5. Update repository list in `apt`
   > sudo apt update

6. Install docker along with its dependencies
   > sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

7. Run docker with default test image
   > sudo docker run hello-world
