## Install Azure CLI
   sudo apt-get update && sudo apt-get install -y gnupg software-properties-common <br>
   wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null<br>
   gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint<br>
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list<br>
   sudo apt update<br>
   sudo apt install terraform<br>
   sudo apt-get update<br>
   sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release<br>
   sudo mkdir -p /etc/apt/keyrings<br>
   curl -sLS https://packages.microsoft.com/keys/microsoft.asc |   gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null<br>
   sudo chmod go+r /etc/apt/keyrings/microsoft.gpg<br>
   AZ_DIST=$(lsb_release -cs)<br>
   echo "Types: deb<br>
   URIs: https://packages.microsoft.com/repos/azure-cli/<br>
   Suites: ${AZ_DIST}<br>
   Components: main<br>
   Architectures: $(dpkg --print-architecture)<br>
   Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources<br>
   sudo apt-get update<br>
   sudo apt-get install azure-cli<br>
   az login<br>
## Generate ssh keys
   ssh-keygen -t ecdsa -b 521<br>
   cat .ssh/id_ecdsa.pub <br>
## Generate RSA Keys and instruct git to sign commits
   gpg --full-generate-key<br>
   gpg --list-secret-keys --keyid-format=long<br>
   gpg --armor --export 921DBD7E8B891C11AE0C5F93CBB681B6338C3826<br>
   git config --global user.signingkey 921DBD7E8B891C11AE0C5F93CBB681B6338C3826<br>
   git config --global commit.gpgsign true<br>
   git config --global tag.gpgSign true<br>
   export GPG_TTY=$(tty)<br>
## Install Kubectl
   curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg<br>
   sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg<br>
   echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list<br>
   sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list<br>
   sudo apt-get update<br>
   sudo apt-get install kubectl<br>
## Get Kubeconfig
   terraform output -raw kube_config > ~/.kube/config<br>
   chmod 600 ~/.kube/config<br>
