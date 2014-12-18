Docker pull into a save

This containerizes the docker pull and outputs
a tar file suitable for 'docker load'.

Usage:
 $ docker run ewindisch/docker-pull ewindisch/trinity | docker load
