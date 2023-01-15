1. git clone https://github.com/amaresh435/new_relic_springboot_web_app.git
2. cd new_relic_springboot_web_app/new_relic
3. sudo docker build -t sb_web_app_image .
4. check with "sudo docker images"  , u will see sb_web_app_image
5. sudo docker run -p 8080:8080 -e NEW_RELIC_APP_NAME="my-application" --name sb_web_application -it sb_web_app_image:latest
6. sudo docker run -p 8080:8080 -e NEW_RELIC_APP_NAME="my-application" --name sb_web_application -itd sb_web_app_image:latest   {add tag -d if required in detach mode}
7. sudo docker run -d --name sb_web_application --network=host --privileged -p 8080:8080 -v "/:/host:ro" -v "/var/run/docker.sock:/var/run/docker.sock" sb_web_app_image:latest
8. check with "sudo docker ps -a"
