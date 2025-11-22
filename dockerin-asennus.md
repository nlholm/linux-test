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

# Kikkailua

## nginx

1. sudo docker run -d -p 8080:80 nginx
2. avaa nettiselain ja mene osoitteeseen: localhost:8080
3. pitäisi näkyä welcome to nginx!
4. Nyt voit luoda muutaman kontin lisää esim -> sudo docker run -d -p 8081:80 nginx -> sudo docker run -d -p 8082:80 nginx
5. katsoa niiden tilat komennolla sudo docker ps
6. seuraavaksi pysäytetään jo poistetaan kontit
7. sudo docker stop [nimi]
8. sudo docker rm [nimi]

https://hub.docker.com/_/nginx

### Muokataan etusivu

1. mkdir /home/user/nginx-demo/sites
2. cd sites
3. index.html
4. cd ..
5. pwd
6. /home/user/nginx-demo/
7. nano docker-compose.yml
```
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - ./site:/usr/share/nginx/html:ro
```
8. sudo docker compose up -d (tämä ajetaan tuolla projektikansiossa)
9. nyt näkyy selaimessa uusi sivu defaultin tilalla

Tätä voisi koittaa automatisoida Saltilla seuraavaksi


https://saikiranpikili.medium.com/building-your-monitoring-stack-automating-docker-installation-with-saltstack-9d352d8e14ad  <- maksumuurin takana, mut jotain ideaa vois saada
