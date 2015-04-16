Docker pull into a save

This containerizes the docker pull and outputs
a tar file suitable for 'docker load'.

Uses:
-----

* Containerizing the public network-facing portions of Docker pulls
* Support pulling from insecure registries on unmodified Docker Engines
* Support image format changes on older Docker Engine releases
  (the save/load format has not changed as commonly as the registry API)

Typical Usage
-------------

```
Command:
 $ docker run ewindisch/docker-pull ewindisch/trinity | docker load
```

This command containerizes the pulling of a container, with loading
and extracting of the tar files on the host's docker daemon.

It's not incredibly efficient as tar files are extracted and
recreated locally. However, malicious tar file extraction is
contained, with a known Docker Engine creating the tar files
to be extracted on the host.

A malicious attacker could still exploit the nested Docker
daemon which performs the network traffic, but this makes
an attack more complex.

Pulling from Insecure Registries
--------------------------------

This image may be useful for pulling from an insecure registry without
reconfiguring the Docker Engine.

Pulling from an insecure registry may be performed with:

```
 $ docker run ewindisch/docker-pull --insecure-registry 10.0.0.0/16 10.0.1.2/someimage | docker load
```

A shortcut for allowing all registries over HTTP is available:

```
 $ docker run ewindisch/docker-pull --insecure 10.0.1.2/someimage | docker load
```

It is NOT advised to use the insecure registry feature as it allows
man-in-the-middle attacks against your infrastructure.
