1. Fix the docker socket  socket issue.   

   1. ``` Cannot connect to the Docker daemon at unix:///Users/achattopadh5/.docker/run/docker.sock. Is the docker daemon running?```
  
        Solution: 
         * Go to ~/.docker
         * Open `config.json`.
         * Remove this line `	"currentContext": "desktop-linux",`.
         * Restart the docker desktop.
     2. ```ERROR: error getting credentials - err: exec: "docker-credential-desktop": executable file not found in $PATH, out: ```
         * Go to ~/.docker
         * Open `config.json`.
         * Update "credsStore" to "credStore"
          

2. Building istio : `BUILD_WITH_CONTAINER=1 make docker`
3. Building only pilot image : `BUILD_WITH_CONTINER=1 make pilot.docker`
4. Build and push the pilot image : `BUILD_WITH_CONTAINER=1 make  pilot.docker.push`


While working with `kind local registry` make sure the hub is `localhost:5001`  but __NOT__ `localhost:5000`.

