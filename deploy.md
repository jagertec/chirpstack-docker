# on localhost:
docker-compose up

docker tag chirpstack/chirpstack-application-server:3 localhost:5000/chirpstack-application-server:3
docker tag chirpstack/chirpstack-gateway-bridge:3 localhost:5000/chirpstack-gateway-bridge:3
docker tag eclipse-mosquitto:2 localhost:5000/eclipse-mosquitto:2
docker tag postgres:9.6-alpine localhost:5000/postgres:9.6-alpine
docker tag redis:5-alpine localhost:5000/redis:5-alpine

docker push localhost:5000/chirpstack-application-server:3
docker push localhost:5000/chirpstack-gateway-bridge:3
docker push localhost:5000/eclipse-mosquitto:2
docker push localhost:5000/postgres:9.6-alpine
docker push localhost:5000/redis:5-alpine

scp -r configuration pi@192.168.1.120:~
scp docker-compose.yml pi@192.168.1.120:~

# on target host:
(https://stackoverflow.com/questions/69831915/docker-compose-error-line-1-not-command-not-found-when-executing-version)
docker-compose up
ggf. docker-compose up --build (wenn die Datenbank nicht neu initialisiert wird)


<!-- echo "starts MeterApi Update on PI"
#docker stop /MeterApi
docker rm --force /MeterApi
#docker rm $(docker ps -a -q)
docker pull 192.168.1.61:5000/meterapi
docker run -it -d -p 8080:8080 --name MeterApi --restart always --device=/dev/ttyUSB0 --privileged 192.168.1.61:5000/meterapi
echo "PI.MeterApi is up to date and running" -->