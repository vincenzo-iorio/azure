## Install Terrafor and AzureCLI
   11  sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
   12  wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
   13  gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
   14  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
   15  sudo apt update
   16  sudo apt install terraform
   18  sudo apt-get update
   19  sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
   20  sudo mkdir -p /etc/apt/keyrings
   21  curl -sLS https://packages.microsoft.com/keys/microsoft.asc |   gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
   22  sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
   23  AZ_DIST=$(lsb_release -cs)
   24  echo "Types: deb
   25  URIs: https://packages.microsoft.com/repos/azure-cli/
   26  Suites: ${AZ_DIST}
   27  Components: main
   28  Architectures: $(dpkg --print-architecture)
   29  Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources
   30  sudo apt-get update
   31  sudo apt-get install azure-cli
   32  az login
## Generate ssh keys
   75  ssh-keygen -t ecdsa -b 521
   77  cat .ssh/id_ecdsa.pub 
## Generate RSA Keys and instruct git to sign commits
   79  gpg --full-generate-key
   80  gpg --list-secret-keys --keyid-format=long
   81  gpg --armor --export 921DBD7E8B891C11AE0C5F93CBB681B6338C3826
   82  git config --global user.signingkey 921DBD7E8B891C11AE0C5F93CBB681B6338C3826
   83  git config --global commit.gpgsign true
   84  git config --global tag.gpgSign true
