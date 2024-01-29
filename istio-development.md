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

2. Running integration test against local kind container
```bash
prow/integ-suite-kind.sh test.integration.pilot.kube
```

3. Running the unit test.
  
   1. Log into docker container. `make shell`  and then copy the `docker-config.json` to  `~/.docker/config.json`
   2. Run the unit test in the folder by running `go test ` or `go test -v `(for verbose mode).
   3. Usually some components re independent of  any other component, like `pilot/pkg/server`. We can run the test  by going into the folder and then running `go test` but that won't work for tests that have dependency on other packages. To test them, just use `go test ...`. 





4. Only build pilot and push that to local repo.

   1. Make sure the `HUB` and `TAG` are set. My local system looks like, 
   
         ```bash
         C02G6ADGMD6R@achattopadh5[linux_amd64](add-tests-for-instance)echo $HUB
         localhost:5000
         C02G6ADGMD6R@achattopadh5[linux_amd64](add-tests-for-instance)echo $TAG
         arijit-test
         ```
   
   2. Then run `make shell` to  things from the build container.
   
        ```bash
        BUILD_ALL=false DOCKER_TARGETS=docker.pilot make dockerx.pushx
        ```
