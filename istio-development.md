1, Fix the docker socket  socket issue. 
Problem message :
``` Cannot connect to the Docker daemon at unix:///Users/achattopadh5/.docker/run/docker.sock. Is the docker daemon running?```

Solution: 
 1. Go to ~/.docker
 2. Open `config.json`.
 3. Remove this line `	"currentContext": "desktop-linux",`.
 4. Restart the docker desktop.
