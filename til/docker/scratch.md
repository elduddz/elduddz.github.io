docker build -t simple-nuget-server . (. loads the dockerfile nearby)

docker images ls

docker run -d -p 80:80 --name nuget free-nuget-server:latest --restart="always"

docker ps