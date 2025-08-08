## Install Terrafor and AzureCLI
   sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
   wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
   gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
   sudo apt update
   sudo apt install terraform
   sudo apt-get update
   sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
   sudo mkdir -p /etc/apt/keyrings
   curl -sLS https://packages.microsoft.com/keys/microsoft.asc |   gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
   sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
   AZ_DIST=$(lsb_release -cs)
   echo "Types: deb
   URIs: https://packages.microsoft.com/repos/azure-cli/
   Suites: ${AZ_DIST}
   Components: main
   Architectures: $(dpkg --print-architecture)
   Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources
   sudo apt-get update
   sudo apt-get install azure-cli
   az login
## Generate ssh keys
   ssh-keygen -t ecdsa -b 521
   cat .ssh/id_ecdsa.pub 
## Generate RSA Keys and instruct git to sign commits
   gpg --full-generate-key
   gpg --list-secret-keys --keyid-format=long
   gpg --armor --export 921DBD7E8B891C11AE0C5F93CBB681B6338C3826
   git config --global user.signingkey 921DBD7E8B891C11AE0C5F93CBB681B6338C3826
   git config --global commit.gpgsign true
   git config --global tag.gpgSign true
   git config --global gpg.program $(which gpg)
   export GPG_TTY=$(tty)
