# Dockerin asennus Debianille

1. sudo apt-get update
2. sudo apt install ca-certificates curl
3. sudo install -m 0755 -d /etc/apt/keyrings
4. sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
5. sudo chmod a+r /etc/apt/keyrings/docker.asc
6. sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF  
7. sudo apt-get update
8. sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
9. sudo systemctl status docker
10. sudo docker run hello-world

https://docs.docker.com/engine/install/debian/#install-using-the-repository

Hyvin näytti toimivan. Huom. jos käytämme Vagranttia ja asennamme bookwormin, niin tuo asennus ei ihan toimi sellaisenaan.
Mutta tuolla sivulla taisi olla ohje millä haetaan asennus tiettyyn versioon.
