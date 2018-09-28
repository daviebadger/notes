========
 Docker
========
-----------------------------------------
 Platforma pro kontejnerizované aplikace
-----------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   $ sudo add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable'
   $ sudo apt update
   $ sudo apt install docker-ce

.. note::

   Pro komunikaci s Dockerem démonem je třeba mít administrátorské oprávnění::

      $ docker version
      Client:
       Version:      18.03.1-ce
       API version:  1.37
       Go version:   go1.9.5
       Git commit:   9ee9f40
       Built:        Thu Apr 26 07:17:38 2018
       OS/Arch:      linux/amd64
       Experimental: false
       Orchestrator: swarm
      Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.37/version: dial unix /var/run/docker.sock: connect: permission denied
      $ sudo docker version
      Client:
       Version:      18.03.1-ce
       API version:  1.37
       Go version:   go1.9.5
       Git commit:   9ee9f40
       Built:        Thu Apr 26 07:17:38 2018
       OS/Arch:      linux/amd64
       Experimental: false
       Orchestrator: swarm

      Server:
       Engine:
        Version:      18.03.1-ce
        API version:  1.37 (minimum version 1.12)
        Go version:   go1.9.5
        Git commit:   9ee9f40
        Built:        Thu Apr 26 07:15:45 2018
        OS/Arch:      linux/amd64
        Experimental: false

.. tip::

   Přidej uživatele do ``docker`` skupiny pro zamezení nutnosti používat
   ``sudo`` příkaz::

      $ sudo usermod -aG docker $USER

   Poté je třeba se odhlásit a znova přihlásit. Alternativně lze v terminálu
   vytvořit novou session pomocí opětovného přihlášení na sebe::

      $ su - $USER
      $ docker --version
      Docker version 18.03.1-ce, build 9ee9f40
      $ docker version
      Client:
       Version:      18.03.1-ce
       API version:  1.37
       Go version:   go1.9.5
       Git commit:   9ee9f40
       Built:        Thu Apr 26 07:17:38 2018
       OS/Arch:      linux/amd64
       Experimental: false
       Orchestrator: swarm

      Server:
       Engine:
        Version:      18.03.1-ce
        API version:  1.37 (minimum version 1.12)
        Go version:   go1.9.5
        Git commit:   9ee9f40
        Built:        Thu Apr 26 07:15:45 2018
        OS/Arch:      linux/amd64
        Experimental: false
      $ exit
      $ docker version
      Client:
       Version:      18.03.1-ce
       API version:  1.37
       Go version:   go1.9.5
       Git commit:   9ee9f40
       Built:        Thu Apr 26 07:17:38 2018
       OS/Arch:      linux/amd64
       Experimental: false
       Orchestrator: swarm
      Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.37/version: dial unix /var/run/docker.sock: connect: permission denied

Příkazy
=======

docker
------

Zobraz nápovědu::

   $ docker

   Usage:	docker COMMAND

   A self-sufficient runtime for containers

   Options:
         --config string      Location of client config files (default "/home/davie/.docker")
     -D, --debug              Enable debug mode
     -H, --host list          Daemon socket(s) to connect to
     -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
         --tls                Use TLS; implied by --tlsverify
         --tlscacert string   Trust certs signed only by this CA (default "/home/davie/.docker/ca.pem")
         --tlscert string     Path to TLS certificate file (default "/home/davie/.docker/cert.pem")
         --tlskey string      Path to TLS key file (default "/home/davie/.docker/key.pem")
         --tlsverify          Use TLS and verify the remote
     -v, --version            Print version information and quit

   Management Commands:
     config      Manage Docker configs
     container   Manage containers
     image       Manage images
     network     Manage networks
     node        Manage Swarm nodes
     plugin      Manage plugins
     secret      Manage Docker secrets
     service     Manage services
     swarm       Manage Swarm
     system      Manage Docker
     trust       Manage trust on Docker images
     volume      Manage volumes

   Commands:
     attach      Attach local standard input, output, and error streams to a running container
     build       Build an image from a Dockerfile
     commit      Create a new image from a container's changes
     cp          Copy files/folders between a container and the local filesystem
     create      Create a new container
     diff        Inspect changes to files or directories on a container's filesystem
     events      Get real time events from the server
     exec        Run a command in a running container
     export      Export a container's filesystem as a tar archive
     history     Show the history of an image
     images      List images
     import      Import the contents from a tarball to create a filesystem image
     info        Display system-wide information
     inspect     Return low-level information on Docker objects
     kill        Kill one or more running containers
     load        Load an image from a tar archive or STDIN
     login       Log in to a Docker registry
     logout      Log out from a Docker registry
     logs        Fetch the logs of a container
     pause       Pause all processes within one or more containers
     port        List port mappings or a specific mapping for the container
     ps          List containers
     pull        Pull an image or a repository from a registry
     push        Push an image or a repository to a registry
     rename      Rename a container
     restart     Restart one or more containers
     rm          Remove one or more containers
     rmi         Remove one or more images
     run         Run a command in a new container
     save        Save one or more images to a tar archive (streamed to STDOUT by default)
     search      Search the Docker Hub for images
     start       Start one or more stopped containers
     stats       Display a live stream of container(s) resource usage statistics
     stop        Stop one or more running containers
     tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
     top         Display the running processes of a container
     unpause     Unpause all processes within one or more containers
     update      Update configuration of one or more containers
     version     Show the Docker version information
     wait        Block until one or more containers stop, then print their exit codes

   Run 'docker COMMAND --help' for more information on a command.

.. note::

   Totožná nápověda se zobrazi pomocí klasické volby ``--help``::

      $ docker --help

pull
^^^^

Stáhni nejnovější ``latest`` obraz z veřejného Docker Hub registru::

   $ docker pull hello-world
   Using default tag: latest
   latest: Pulling from library/hello-world
   9bb5a5d4561a: Pull complete
   Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
   Status: Downloaded newer image for hello-world:latest

Stáhni obraz s konkrétním tagem z veřejného Docker Hubu::

   $ docker pull ubuntu:16.04

Stáhni obraz s konkrétním tagem z konkrétního repozitáře zveřejného Docker
Hubu::

   $ docker pull pivotaldata/ubuntu:16.04

Stáhni obraz z vlastního registru::

   $ docker pull localhost:5000/image

.. note::

   Pokud se vlastní repozitář nachází ve vnitřní síti a navíc nemá SSL
   certifikát, pak je třeba nakonfigurovat Docker démona, aby nevznikal error
   x509, který prověřuje platnost a validitu certifikátu pro SSL zabezpečení::

      $ sudo cat /etc/docker/daemon.json
      {
        "dns": ["1.2.3.4"],
        "insecure-registry": [
          "myregistry:5000"
        ]
      }

.. tip::

   Každý stáhnutý obraz má svůj ``sha256`` hash v klíči ``Digest``, pomocí
   kterého lze identifikovat konkrétní verzi obrazu, neboť pod tagy se mohou
   obrazy měnit v repozitáři::

      $ docker pull hello-world@sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77

images
^^^^^^

Zobraz seznam lokálních obrazů::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   hello-world         latest              e38bc07ac18e        5 weeks ago         1.85kB

.. tip::

   Vyfiltruj seznam lokálních obrazů::

      $ docker images *ello*
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      hello-world         latest              e38bc07ac18e        5 weeks ago         1.85kB

images -a
"""""""""

Zobraz seznam lokálních obrazů včetně nakešovaných vrstev (intermediate
obrazy)::

   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build -t python-test .
   Sending build context to Docker daemon  6.681MB
   Step 1/2 : FROM python:3-alpine
   3-alpine: Pulling from library/python
   ff3a5c916c92: Already exists
   471170bb1257: Already exists
   a92899abaf42: Already exists
   2699438859de: Already exists
   d278818cf042: Already exists
   Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
   Status: Downloaded newer image for python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in a57fd788cafd
   Removing intermediate container a57fd788cafd
    ---> 8ac190dc05fa
   Successfully built 8ac190dc05fa
   Successfully tagged python-test:latest
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              8ac190dc05fa        29 seconds ago      87.4MB
   python              3-alpine            27e79c0fa4d2        4 weeks ago         87.4MB
   $ tail -1 Dockerfile >> Dockerfile
   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build -t python-test .
   Sending build context to Docker daemon  6.681MB
   Step 1/3 : FROM python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/3 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Using cache
    ---> 8ac190dc05fa
   Step 3/3 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in 41741160766a
   Removing intermediate container 41741160766a
    ---> b020d94e2719
   Successfully built b020d94e2719
   Successfully tagged python-test:latest
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              b020d94e2719        24 seconds ago      87.4MB
   python              3-alpine            27e79c0fa4d2        4 weeks ago         87.4MB
   $ docker images -a
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              b020d94e2719        40 seconds ago      87.4MB
   <none>              <none>              8ac190dc05fa        2 minutes ago       87.4MB
   python              3-alpine            27e79c0fa4d2        4 weeks ago         87.4MB

.. note::

   Intermediate obrazy mohou vznikat i při pullování, kdy v novějším obrazu
   vzniknou další vrstvy, pričemž předchozí vrstvy se nakešují a znovupoužijí
   jako závislosti.

   Starší obraz se jednak označí jako rodič, na kterém je navázana závislost na
   novější dětský obraz, a druhak bude tento obraz zobrazen ve výpisu obrazů
   jako ``<none>:<none>``, kdežto novější obraz převezme původní označení.

images --digests
""""""""""""""""

Zobraz seznam lokálních obrazů včetně digestů::

   $ docker images --digests
   REPOSITORY          TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
   hello-world         latest              sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77   e38bc07ac18e        6 weeks ago         1.85kB

images -f
"""""""""

Zobraz seznam nepojmenovaných lokálních obrazů::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build .
   Sending build context to Docker daemon  6.684MB
   Step 1/2 : FROM python:3-alpine
   3-alpine: Pulling from library/python
   ff3a5c916c92: Already exists
   471170bb1257: Already exists
   a92899abaf42: Already exists
   2699438859de: Already exists
   d278818cf042: Already exists
   Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
   Status: Downloaded newer image for python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in 406e241bc2be
   Removing intermediate container 406e241bc2be
    ---> c43c34f7551d
   Successfully built c43c34f7551d
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   <none>              <none>              c43c34f7551d        14 seconds ago      87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker images -f 'dangling=true'
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   <none>              <none>              c43c34f7551d        3 minutes ago       87.4MB

Zobraz seznam nepojmenovaných lokálních obrazů::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build -t python-test .
   Sending build context to Docker daemon  6.687MB
   Step 1/2 : FROM python:3-alpine
   3-alpine: Pulling from library/python
   ff3a5c916c92: Already exists
   471170bb1257: Already exists
   a92899abaf42: Already exists
   2699438859de: Already exists
   d278818cf042: Already exists
   Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
   Status: Downloaded newer image for python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in 6c2f9fea60ac
   Removing intermediate container 6c2f9fea60ac
    ---> 320192481d5f
   Successfully built 320192481d5f
   Successfully tagged python-test:latest
   $ sed -i 's/World/Davie/' Dockerfile
   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello Davie!')"]
   $ docker build -t python-test .
   Sending build context to Docker daemon  6.687MB
   Step 1/2 : FROM python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello Davie!')"]
    ---> Running in 56dd9b14ad0f
   Removing intermediate container 56dd9b14ad0f
    ---> 82727637a829
   Successfully built 82727637a829
   Successfully tagged python-test:latest
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
   python-test         latest              82727637a829        17 seconds ago       87.4MB
   <none>              <none>              320192481d5f        About a minute ago   87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago          87.4MB
   $ docker images -f 'dangling=true'
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   <none>              <none>              320192481d5f        2 minutes ago       87.4MB

.. note::

   Dangling obrazy je třeba pravidelně mazat, neboť na rozdíl od intermediate
   obrazů nemají žádné vazby na jiné obrazy / vrstvy a zbytečně zabírají místo
   na disku.

images -q
"""""""""

Zobraz seznam lokálních obrazů podle jejich ID::

   $ docker images -q
   e38bc07ac18e

build
^^^^^

Vytvoř nepojmenovaný obraz z ``Dockerfile`` souboru::

   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build .
   Sending build context to Docker daemon  6.684MB
   Step 1/2 : FROM python:3-alpine
   3-alpine: Pulling from library/python
   ff3a5c916c92: Already exists
   471170bb1257: Already exists
   a92899abaf42: Already exists
   2699438859de: Already exists
   d278818cf042: Already exists
   Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
   Status: Downloaded newer image for python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in 406e241bc2be
   Removing intermediate container 406e241bc2be
    ---> c43c34f7551d
   Successfully built c43c34f7551d
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   <none>              <none>              c43c34f7551d        14 seconds ago      87.4MB

.. tip::

   Pomocí ``.dockerignore`` souboru (stejný princip jako ``.gitignore`` v Gitu)
   lze urychlit vytváření obrazů, neboť defaultně se do Docker démonu posílá
   celý kontext adresáře obsahující ``Dockerfile`` pro možné pozdější použití::

      $ docker build .
      Sending build context to Docker daemon  6.689MB
      Step 1/2 : FROM python:3-alpine
      3-alpine: Pulling from library/python
      ff3a5c916c92: Already exists
      471170bb1257: Already exists
      a92899abaf42: Already exists
      2699438859de: Already exists
      d278818cf042: Already exists
      Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
      Status: Downloaded newer image for python:3-alpine
       ---> 27e79c0fa4d2
      Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
       ---> Running in de89ff42a1e1
      Removing intermediate container de89ff42a1e1
       ---> 540305bb23fa
      Successfully built 540305bb23fa
      $ echo '.git' > .dockerignore
      $ docker build .
      Sending build context to Docker daemon  695.3kB
      Step 1/2 : FROM python:3-alpine
       ---> 27e79c0fa4d2
      Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
       ---> Using cache
       ---> 540305bb23fa
      Successfully built 540305bb23fa

Odbočka k Dockerfile souboru
""""""""""""""""""""""""""""

Vytvoř vlastní obraz s jednoduchou Flask aplikací::

   $ ls
   app.py  Dockerfile  requirements.txt
   $ cat app.py
   import os

   from flask import Flask

   app = Flask(__name__)


   @app.route("/")
   def hello():
       name = os.environ.get("NAME")

       return f"Hello {name}!"


   if __name__ == "__main__":
       app.run(host="0.0.0.0")
   $ cat requirements.txt
   flask
   $ cat Dockerfile
   FROM python:3.6-alpine

   LABEL maintainer="davie.badger@gmail.com"

   COPY requirements.txt /app/requirements.txt

   WORKDIR /app

   RUN pip install -r requirements.txt \
       && addgroup -g 1000 -S davie \
       && adduser -u 1000 -G davie -S -h /app davie

   COPY . /app

   USER davie

   ENV NAME=davie

   EXPOSE 5000

   CMD ["python3", "app.py"]
   $ docker build .

.. note::

   Pokud aplikace v kontejneru generuje data za běhu, tak je vhodné je ukládat
   mimo kontejner na hostovaném počítači jako volume pro pozdější obnovu,
   pokud kontejner selže::

      VOLUME ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

.. tip::

   Aby byl build obrazu co nejmenší a nejrychlejší, je třeba správně zvolit
   bázový obraz, vážit pořádí instrukcí a jejich četnost, zejména u ``COPY``
   a ``RUN`` instrukcí, jelikož tyto vrstvy zvětšuji obraz buildu::

      # Alpine Linux
      #
      # apk is package manager for Alpine linux
      #
      # List of packages: https://pkgs.alpinelinux.org/packages

      RUN apk add --no-cache --virtual .build-deps \
              ca-certificates \
              gcc \
              wget \
          && apk del .build-deps

      # Debian / Ubuntu Linux

      RUN apt-get update \
          && apt install -y --no-install-recommends \
              ca-certificates \
              gcc \
              wget \
          && rm -rf /var/lib/apt/lists/*

   Spolu s hromadnými příkazy v jednom ``RUN`` příkazu je vhodné použít i
   příkaz ``set -ex``, který při buildování kontejneru ukáže, který konkrétní
   příkaz se právě vykonává::

      $ cat Dockerfile
      FROM alpine

      RUN set -ex; \
          apk add --no-cache --virtual .build-deps \
              curl \
              make \
              wget \
          ; \
          apk del .build-deps;
      $ docker build .
      Sending build context to Docker daemon  741.4kB
      Step 1/2 : FROM alpine
       ---> 3fd9065eaf02
      Step 2/2 : RUN set -ex;     apk add --no-cache --virtual .build-deps             curl             make             wget     ;     apk del .build-deps;
       ---> Running in 598222f56512
      1. apk add --no-cache --virtual .build-deps curl make wget
      fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/main/x86_64/APKINDEX.tar.gz
      fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/community/x86_64/APKINDEX.tar.gz
      (1/7) Installing ca-certificates (20171114-r0)
      (2/7) Installing libssh2 (1.8.0-r2)
      (3/7) Installing libcurl (7.60.0-r1)
      (4/7) Installing curl (7.60.0-r1)
      (5/7) Installing make (4.2.1-r0)
      (6/7) Installing wget (1.19.5-r0)
      (7/7) Installing .build-deps (0)
      Executing busybox-1.27.2-r7.trigger
      Executing ca-certificates-20171114-r0.trigger
      OK: 6 MiB in 18 packages
      1. apk del .build-deps
      WARNING: Ignoring APKINDEX.70c88391.tar.gz: No such file or directory
      WARNING: Ignoring APKINDEX.5022a8a2.tar.gz: No such file or directory
      (1/7) Purging .build-deps (0)
      (2/7) Purging curl (7.60.0-r1)
      (3/7) Purging make (4.2.1-r0)
      (4/7) Purging wget (1.19.5-r0)
      (5/7) Purging libcurl (7.60.0-r1)
      (6/7) Purging ca-certificates (20171114-r0)
      Executing ca-certificates-20171114-r0.post-deinstall
      (7/7) Purging libssh2 (1.8.0-r2)
      Executing busybox-1.27.2-r7.trigger
      OK: 4 MiB in 11 packages
      Removing intermediate container 598222f56512
        ---> 78f7f8e58091
      Successfully built 78f7f8e58091

build --no-cache
""""""""""""""""

Vytvoř nejpojmenovaný obraz bez cache::

   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build .
   Sending build context to Docker daemon  7.679MB
   Step 1/2 : FROM python:3-alpine
    ---> d30308ec4dc1
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Using cache
    ---> d05cf6f122ac
   Successfully built d05cf6f122ac
   $ docker build --no-cache .
   Sending build context to Docker daemon  7.679MB
   Step 1/2 : FROM python:3-alpine
    ---> d30308ec4dc1
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in c122cdcc8418
   Removing intermediate container c122cdcc8418
    ---> f33e51215c84
   Successfully built f33e51215c84

build -t
""""""""

Vytvoř pojmenovaný obraz z ``Dockerfile`` souboru::

   $ cat Dockerfile
   FROM python:3-alpine

   CMD ["python3", "-c", "print('Hello World!')"]
   $ docker build -t python-test .
   Sending build context to Docker daemon  6.687MB
   Step 1/2 : FROM python:3-alpine
   3-alpine: Pulling from library/python
   ff3a5c916c92: Already exists
   471170bb1257: Already exists
   a92899abaf42: Already exists
   2699438859de: Already exists
   d278818cf042: Already exists
   Digest: sha256:bfac58481666aeb60ff6354e81afe888cc8c7b1effb1039870377fc7fa86ef43
   Status: Downloaded newer image for python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Running in 4d1d02599487
   Removing intermediate container 4d1d02599487
    ---> d5b6cef09caa
   Successfully built d5b6cef09caa
   Successfully tagged python-test:latest
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              d5b6cef09caa        4 seconds ago       87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB

Vytvoř pojmenovaný obraz z ``Dockerfile`` včetně dodatečného tagu::

   $ docker build -t python-test:0.1.0 .
   Sending build context to Docker daemon  6.688MB
   Step 1/2 : FROM python:3-alpine
    ---> 27e79c0fa4d2
   Step 2/2 : CMD ["python3", "-c", "print('Hello World!')"]
    ---> Using cache
    ---> d5b6cef09caa
   Successfully built d5b6cef09caa
   Successfully tagged python-test:0.1.0
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
   python-test         0.1.0               d5b6cef09caa        About a minute ago   87.4MB
   python-test         latest              d5b6cef09caa        About a minute ago   87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago          87.4MB

.. note::

   Pojmenovaný obraz bez dodatečného tagu má automaticky přidělen tag
   ``latest``.

.. tip::

   Obraz lze pojmenovat i pod více nazvy / tagy::

      $ docker build -t python-test:latest python-test:0.1.0

tag
^^^

Otaguj obraz novým alisem::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              a55e2c30d10c        2 seconds ago       87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker tag python-test python-test-test
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test-test    latest              a55e2c30d10c        19 minutes ago      87.4MB
   python-test         latest              a55e2c30d10c        19 minutes ago      87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB

Otaguj obraz novým tagem::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              a55e2c30d10c        2 seconds ago       87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker tag python-test python-test:0.1.0
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         0.1.0               a55e2c30d10c        20 minutes ago      87.4MB
   python-test         latest              a55e2c30d10c        20 minutes ago      87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB

Otaguj obraz repozitářem, alisem a tagem::

   $ docker tag python-test python/python-test:0.1.0

.. note::

   Pro pushování obrazů do vlastního registru je nutné obrazy otagovat včetně
   hostu, respektive i portu::

      $ docker tag a55e2c30d10c localhost:5000/python/python-test

push
^^^^

Nahrej obraz do veřejného repozitáře v Docker Hub registru::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              a55e2c30d10c        About an hour ago   87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker tag python-test daviebadger/python
   $ docker images
   REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
   daviebadger/python   latest              a55e2c30d10c        About an hour ago   87.4MB
   python-test          latest              a55e2c30d10c        About an hour ago   87.4MB
   python               3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker login
   Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
   Username: daviebadger
   Password:
   Login Succeeded
   $ docker push daviebadger/python
   The push refers to repository [docker.io/daviebadger/python]
   869c7a702293: Mounted from library/python
   9e7b1d7a3bd9: Mounted from library/python
   03123738fe33: Mounted from library/python
   6b68dfad3e66: Mounted from library/python
   cd7100a72410: Mounted from library/python
   latest: digest: sha256:a7467d1abd407f4a152372f9393faab8cde9d0233cab34ac82eae87f87eb3dd3 size: 1368
   $ docker rmi daviebadger/python
   $ docker pull daviebadger/python
   Using default tag: latest
   latest: Pulling from daviebadger/python
   Digest: sha256:a7467d1abd407f4a152372f9393faab8cde9d0233cab34ac82eae87f87eb3dd3
   Status: Downloaded newer image for daviebadger/python:latest

Nahrej obraz do vlastního registru::

   $ docker tag python-test localhost:5000/python-test
   $ docker push localhost:5000/python-test

Nahrej obraz do vlastního repozitáře ve vlastním registru::

   $ docker tag python-test localhost:5000/daviebadger/python-test
   $ docker push localhost:5000/daviebadgerpython-test

.. note::

   Pro pushování obrazů do registrů je třeba být přihlášen pomocí příkazu
   ``docker login``. V případě vlastního registru je třeba uvést explicitně
   tento registr v rámci přihlášení::

      $ docker login localhost:5000

   V případě automatických skriptů lze pomocí voleb uvést uživatele a heslo::

      $ docker login -u daviebadger -p password

   Přihlašovací token se uloží do ``~/.docker/config.json``, dokud nedojde k
   odhlášení::

      $ docker logout  # or docker logout localhost:5000
      Removing login credentials for https://index.docker.io/v1/
      $ cat ~/.docker/config.json
      {
         "auths": {},
         "HttpHeaders": {
            "User-Agent": "Docker-Client/18.03.1-ce (linux)"
         }
      }

rmi
^^^

Smaž konkrétní obraz s výchozím ``latest`` tagem::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   hello-world         latest              e38bc07ac18e        6 weeks ago         1.85kB
   $ docker rmi hello-world
   Untagged: hello-world:latest
   Untagged: hello-world@sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
   Deleted: sha256:e38bc07ac18ee64e6d59cf2eafcdddf9cec2364dfe129fe0af75f1b0194e0c96
   Deleted: sha256:2b8cbd0846c5aeaa7265323e7cf085779eaf244ccbdd982c4931aef9be0d2faf
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

Smaž konkrétní obraz s daným tagem::

   $ docker rmi python:3-alpine

Smaž konkrétní nepojmenovaný obraz podle jeho ID::

   $ docker images 19aee84d327e

Smaž všechny dangling obrazy::

   $ docker rmi $(docker images -f 'dangling=true' -q)

Smaž všechny obrazy::

   $ docker rmi $(docker images -q)

.. note::

   Pokud existují kontejnery pro daný obraz, tak tento obraz nepůjde smazat::

      $ docker images
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      hello-world         latest              e38bc07ac18e        6 weeks ago         1.85kB
      $ docker run hello-world
      $ docker rmi hello-world
      Error response from daemon: conflict: unable to remove repository reference "hello-world" (must force) - container 5d1acbd25c8f is using its referenced image e38bc07ac18e

   Taktéž nepůjdou smazat mangling obrazy::

      $ docker images -a
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      python-test         latest              cf588e648145        3 seconds ago       87.4MB
      <none>              <none>              0976e00efc5f        18 seconds ago      87.4MB
      python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
      $ docker rmi 0976e00efc5f
      Error response from daemon: conflict: unable to delete 0976e00efc5f (cannot be forced) - image has dependent child images

.. tip::

   Jako ID obrazu lze použít i prvních pár znaků::

      $ docker images
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      hello-world         latest              e38bc07ac18e        6 weeks ago         1.85kB
      $ docker rmi e
      $ docker images
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

rmi -f
""""""

Smaž násilně obrazy, kterém mají shodné ID::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              02bc6b2561fc        2 minutes ago       87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker tag python-test python-test1
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python-test         latest              02bc6b2561fc        2 minutes ago       87.4MB
   python-test1        latest              02bc6b2561fc        2 minutes ago       87.4MB
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB
   $ docker rmi 02bc6b2561fc
   Error response from daemon: conflict: unable to delete 02bc6b2561fc (must be forced) - image is referenced in multiple repositories
   $ docker rmi -f 02bc6b2561fc
   Untagged: python-test1:latest
   Untagged: python-test:latest
   Deleted: sha256:02bc6b2561fcbdeadd3c7df108288b8148738b3b84aec2dd1ba17a5d4640cae6
   Deleted: sha256:8f7350f3e54317ef44fbda1dc6deab12d056094c687a9f0107ed92b14271611b
   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   python              3-alpine            27e79c0fa4d2        5 weeks ago         87.4MB

create
^^^^^^

Vytvoř nový nepojmenovaný kontejner z daného obrazu::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   hello-world         latest              e38bc07ac18e        6 weeks ago         1.85kB
   $ docker create hello-world
   d7d1cb5cd6e01350bfae95f4331d3620fee537c3aa1f290b8972effe91f74cd0
   $ docker ps -a
   CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   09db668cb007        hello-world         "/hello"            3 seconds ago       Created                                 blissful_volhard

.. note::

   Pokud obraz neexistuje lokálně, tak se Docker pokusí pullnost obraz z
   veřejného registru::

      $ docker images
      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      $ docker create hello-world
      Unable to find image 'hello-world:latest' locally
      latest: Pulling from library/hello-world
      9bb5a5d4561a: Pull complete
      Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
      Status: Downloaded newer image for hello-world:latest
      20995e7ec95b360dfea7ed756b58061248768ceb6c5aa84f297daf0d68669a19

.. tip::

   Vytvoř nový nepojmenovaný kontejner z daného obrazu a při nastartování
   kontejneru spusť konkrétní příkaz::

      $ docker create alpine ls -l
      $ docker create -it alpine /bin/sh
      $ docker create -it ubuntu /bin/bash

   Příkaz poslaný do vytvořeného kontejneru přepíše příkaz ``CMD`` v obrazu,
   pokud se nachází. Je-li v obrazu příkaz ``ENTRYPOINT`` (nedoporučuje se),
   tak se příkaz nepřepíše a spustí se až za ním.

create -e
"""""""""

Vytvoř nový nepojmenovaný kontejner a pošli do něj jednorázově hodnotu proměnné
z shellu::

   $ echo $USER
   davie
   $ docker create -e DOCKER_USER=$USER

.. note::

   Pokud v shellu daná proměnné neexistuje, tak se do kontejneru pošle jako
   její obsah prázdný řetězec.

.. tip::

   Do kontejneru lze poslat několik proměnných::

      $ docker create -e ONE=1 TWO=2 THREE=3

create -it
""""""""""

Vytvoř nový nepojmenovaný kontejner včetně interaktivní komunikace a textové
konzole pro komunikaci s kontejnerem přes příkazový řádek::

   $ docker create -it python-test

create --name
"""""""""""""

Vytvoř nový pojmenovaný kontejner z daného obrazu::

   $ docker create --name davie hello-world
   1d4db2f1ae5be90be6ad104983da50f48a2a223ba1f1e7f589ffadd7c3bad106
   $ docker ps -a
   CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
   1d4db2f1ae5b        hello-world         "/hello"            25 seconds ago      Created                                 davie

.. note::

   Nepojmenované kontejnery mají také jméno, které se generuje náhodně, např.
   ``blissful_volhard``.

create -p
"""""""""

Vytvoř nový nepojmenovaný kontejner a propoj lokální port s portem uvnitř kontejneru::

   $ docker create -p 8000:80 nginx

.. note::

   V obrazu musí být explicitně vystaven daný port ven pomocí ``EXPOSE``
   příkazu.

create --restart
""""""""""""""""

Vytvoř nový nepojmenovaný kontejner, který se restartuje, pokud hlavní příkaz
selže::

   $ docker create --restart on-failure python-test

Vytvoř nový nepojmenovaný kontejner, který se restartuje, ať už je exitový
kód hlavního příkazu jakýkoliv::

   $ docker create --restart always python-test

.. note::

   Pokud je kontejner nebo Docker démon pozastaven, tak se kontejner nebude
   restartovat, je-li použit argument ``unless-stopped``::

      $ docker create --restart unless-stopped python-test

create --rm
"""""""""""

Vytvoř nový nepojmenovaný kontejner, který se automaticky smaže, jakmile se
kontejner ukončí (exituje)::

   $ docker create --rm hello-world
   0e72f115dc3e7b18baeededf84f6c0858279681dcfcfa67194c75252ba91e1cb

.. note::

   Pokud má kontejner vytvořen volume, tak se po smazání kontejneru smaže i to.

create -v
"""""""""

Vytvoř nový nepojmenovaný kontejner s nepojmenovaným volume adresářem::

   $ docker create -v /data test

Vytvoř nový nepojmenovaný kontejner s pojmenovaným volume adresářem::

   $ docker create -v data:/data test

Vytvoř nový nepojmenovaný kontejner, který propojí lokální adresář s adresářem
v kontejneru::

   $ docker create -v /home/davie/test:/test alpine

.. note::

   Změna v lokálním adresáři se okamžitě projeví i v namontovaném adresáři v
   kontejneru a opačně. Po smazání kontejneru se nesmažou data v lokálním
   adresáři.

create --volumes-from
"""""""""""""""""""""

Vytvoř nový nepojmenovaný kontejner, který napoj na volume v jiném existujícím
kontejneru::

   $ docker create --volumes-from test test-test

.. note::

   Volumy si Docker ukládá do adresáře ``/var/lib/docker/volumes``.

start
^^^^^

Spusť kontejner podle jeho ID::

   $ docker start 0e72f115dc3e

Spusť kontejner podle jeho jména::

   $ docker start frosty_hopper

Spusť několik kontejnerů najednou::

   $ docker start one two three

.. note::

   Pokud příkazy v kontejneru posílájí něco na stdout nebo stderr, tak
   defaultně tyto výstupy nebudou vidět.

start -a
""""""""

Spusť kontejner a připoj jeho stdout/stderr výstupy::

   $ docker start -a suspicious_dijkstra

   Hello from Docker!
   This message shows that your installation appears to be working correctly.

   To generate this message, Docker took the following steps:
    A. The Docker client contacted the Docker daemon.
    B. The Docker daemon pulled the "hello-world" image from the Docker Hub.
       (amd64)
    C. The Docker daemon created a new container from that image which runs the
       executable that produces the output you are currently reading.
    D. The Docker daemon streamed that output to the Docker client, which sent it
       to your terminal.

   To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

   Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

   For more examples and ideas, visit:
    https://docs.docker.com/engine/userguide/

.. note::

   Po stiknutí klávesové zkratky ``CTRL + c`` pro ukončení čtení výstupů
   dojde automaticky k ukončení kontejneru.

.. tip::

   Pomocí klávesové zkratky ``CTRL + p`` a ``CTRL + q`` se lze odpojit
   od čtení výstupů a nechat běžet kontejner na pozadí, akorát je třeba ještě
   použít volbu ``-i`` pro umožnení standardního vstupu::

      $ docker pull nginx:alpine
      $ docker create -it --rm -p 8000:80 -it --name nginx nginx:alpine
      $ docker start -ai
      172.17.0.1 - - [30/May/2018:18:13:02 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
      ^P^C
      read escape sequence

   Aby bylo tohle všechno možné, je třeba ještě mít vytvořený kontejner s
   volbou ``-it``.

start -i
""""""""

Spusť kontejner a připoj jeho stdin vstup::

   $ cat Dockerfile
   FROM python:3-alpine

   COPY test.py .

   CMD ["python3", "test.py"]
   $ cat test.py
   while True:
       input("Your input: ")
   $ docker build -t python-test .
   $ docker create -it --name test python-test
   $ docker start -i test
   Your input: a
   Your input: b
   Your input: c

.. note::

   Kontejner musí být vytvořen s volbou ``-it``, která zajistí interaktivní
   komunikaci s textovou konzolí.

run
^^^

Vytvoř a spusť nový nepojmenovaný kontejner z daného obrazu::

   $ docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   hello-world         latest              e38bc07ac18e        6 weeks ago         1.85kB
   $ docker run hello-world

.. note::

   V příkazu lze použít stejné jako volby, jako pro ``docker create`` příkaz::

      $ docker run -it --rm --name test python-test

run -d
""""""

Vytvoř a spusť nový nepojmenovaný kontejner na pozadí::

   $ docker run -d -p 8000:80 nginx-alpine
   8cf64fbe488a3a5711a88e74225d76994ae1ea912a44f3fe8f3d9a5892cdb7a9

ps
^^

Zobraz seznam běžících kontejnerů::

   $ docker ps
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
   ef45ce5483dc        nginx:alpine        "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes        0.0.0.0:8000->80/tcp   nginx

ps -a
"""""

Zobraz seznam všech běžících i neběžících kontejnerů::

   $ docker ps -a
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS                  NAMES 1791d154758b        hello-world         "/hello"                 3 seconds ago       Exited (0) 1 second ago                          admiring_poincare
   ef45ce5483dc        nginx:alpine        "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes              0.0.0.0:8000->80/tcp   nginx

ps -f
"""""

Zobraz vyfiltrovaný seznam kontejnerů podle statusu::

   $ docker ps -f 'status=running'
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
   ef45ce5483dc        nginx:alpine        "nginx -g 'daemon of…"   3 days ago          Up 2 days           0.0.0.0:8000->80/tcp   nginx

Zobraz vyfiltrovaný seznam kontejnerů podle názvu::

   $ docker ps -f 'name=container'

.. tip::

   Filtry lze kombinovat::

      $ docker ps -f 'status=created' -f 'status=paused' -f 'status=exited'

ps -l
"""""

Zobraz poslední vytvořený kontejner::

   $ docker ps -l
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
   ef45ce5483dc        nginx:alpine        "nginx -g 'daemon of…"   3 days ago          Up 2 days           0.0.0.0:8000->80/tcp   nginx

ps -q
"""""

Zobraz seznam běžících kontejnerů podle jejich ID::

   $ docker images -q
   5d1acbd25c8f

stats
^^^^^

Zobraz aktuální statistiku použití u běžících kontejnerů::

   $ docker stats
   CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
   ef45ce5483dc        nginx               0.00%               1.617MiB / 3.742GiB   0.04%               73.4kB / 1.54kB     25.4MB / 0B         2

Zobraz aktuální statistiku použítí pro konkrétní kontejner::

   $ docker stats nginx
   CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
   ef45ce5483dc        nginx               0.00%               1.617MiB / 3.742GiB   0.04%               73.4kB / 1.54kB     25.4MB / 0B         2

.. note::

   Stream statistik je třeba ukončit pomocí klávesové zkrakty ``CTRL + c ``.

top
^^^

Zobraz běžící procesy v kontejneru::

   $ docker top nginx
   UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
   root                13673               13648               0                   21:39               pts/0               00:00:00            nginx: master process nginx -g daemon off;
   systemd+            13729               13673               0                   21:39               pts/0               00:00:00            nginx: worker process

inspect
^^^^^^^

Zobraz detailní informace o kontejneru::

   $ docker inspect nginx
   [
       {
           "Id": "ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb",
           "Created": "2018-05-30T19:39:38.268160717Z",
           "Path": "nginx",
           "Args": [
               "-g",
               "daemon off;"
           ],
           "State": {
               "Status": "running",
               "Running": true,
               "Paused": false,
               "Restarting": false,
               "OOMKilled": false,
               "Dead": false,
               "Pid": 16878,
               "ExitCode": 0,
               "Error": "",
               "StartedAt": "2018-05-30T20:22:04.88381606Z",
               "FinishedAt": "2018-05-30T20:20:13.858225365Z"
           },
           "Image": "sha256:ebe2c7c61055cae340273904364fd6c6c0e8bab75ef97777263b248264acf3c8",
           "ResolvConfPath": "/var/lib/docker/containers/ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb/resolv.conf",
           "HostnamePath": "/var/lib/docker/containers/ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb/hostname",
           "HostsPath": "/var/lib/docker/containers/ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb/hosts",
           "LogPath": "/var/lib/docker/containers/ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb/ef45ce5483dcfb3bf21bccdf6d6d216cfe8289db11618733c8bf4723e5e317bb-json.log",
           "Name": "/nginx",
           "RestartCount": 0,
           "Driver": "overlay2",
           "Platform": "linux",
           "MountLabel": "",
           "ProcessLabel": "",
           "AppArmorProfile": "docker-default",
           "ExecIDs": null,
           "HostConfig": {
               "Binds": null,
               "ContainerIDFile": "",
               "LogConfig": {
                   "Type": "json-file",
                   "Config": {}
               },
               "NetworkMode": "default",
               "PortBindings": {
                   "80/tcp": [
                       {
                           "HostIp": "",
                           "HostPort": "8000"
                       }
                   ]
               },
               "RestartPolicy": {
                   "Name": "no",
                   "MaximumRetryCount": 0
               },
               "AutoRemove": false,
               "VolumeDriver": "",
               "VolumesFrom": null,
               "CapAdd": null,
               "CapDrop": null,
               "Dns": [],
               "DnsOptions": [],
               "DnsSearch": [],
               "ExtraHosts": null,
               "GroupAdd": null,
               "IpcMode": "shareable",
               "Cgroup": "",
               "Links": null,
               "OomScoreAdj": 0,
               "PidMode": "",
               "Privileged": false,
               "PublishAllPorts": false,
               "ReadonlyRootfs": false,
               "SecurityOpt": null,
               "UTSMode": "",
               "UsernsMode": "",
               "ShmSize": 67108864,
               "Runtime": "runc",
               "ConsoleSize": [
                   0,
                   0
               ],
               "Isolation": "",
               "CpuShares": 0,
               "Memory": 0,
               "NanoCpus": 0,
               "CgroupParent": "",
               "BlkioWeight": 0,
               "BlkioWeightDevice": [],
               "BlkioDeviceReadBps": null,
               "BlkioDeviceWriteBps": null,
               "BlkioDeviceReadIOps": null,
               "BlkioDeviceWriteIOps": null,
               "CpuPeriod": 0,
               "CpuQuota": 0,
               "CpuRealtimePeriod": 0,
               "CpuRealtimeRuntime": 0,
               "CpusetCpus": "",
               "CpusetMems": "",
               "Devices": [],
               "DeviceCgroupRules": null,
               "DiskQuota": 0,
               "KernelMemory": 0,
               "MemoryReservation": 0,
               "MemorySwap": 0,
               "MemorySwappiness": null,
               "OomKillDisable": false,
               "PidsLimit": 0,
               "Ulimits": null,
               "CpuCount": 0,
               "CpuPercent": 0,
               "IOMaximumIOps": 0,
               "IOMaximumBandwidth": 0
           },
           "GraphDriver": {
               "Data": {
                   "LowerDir": "/var/lib/docker/overlay2/c20a680fd52d6645575a08db31e7ff6140e1c69fc8a12e8ddfe2565d1e809be4-init/diff:/var/lib/docker/overlay2/7671cec39fcd9889ece40aefdc3f4d26fe0961fe8c23e610734d6487ef0a4c72/diff:/var/lib/docker/overlay2/077e0dcfc8ea12c32ff2cb3b7dc20ef99921054e4df5474ad5f4c9a977aa52f6/diff:/var/lib/docker/overlay2/a2abd939767e876e316fe33ad7c12f3327cc63cc86a1fb09faaef93942543a24/diff:/var/lib/docker/overlay2/e4e38ba64be46ccbfb86ee0da13cfe95041dce6c3b26408b3490e80fa867ac07/diff",
                   "MergedDir": "/var/lib/docker/overlay2/c20a680fd52d6645575a08db31e7ff6140e1c69fc8a12e8ddfe2565d1e809be4/merged",
                   "UpperDir": "/var/lib/docker/overlay2/c20a680fd52d6645575a08db31e7ff6140e1c69fc8a12e8ddfe2565d1e809be4/diff",
                   "WorkDir": "/var/lib/docker/overlay2/c20a680fd52d6645575a08db31e7ff6140e1c69fc8a12e8ddfe2565d1e809be4/work"
               },
               "Name": "overlay2"
           },
           "Mounts": [],
           "Config": {
               "Hostname": "ef45ce5483dc",
               "Domainname": "",
               "User": "",
               "AttachStdin": false,
               "AttachStdout": false,
               "AttachStderr": false,
               "ExposedPorts": {
                   "80/tcp": {}
               },
               "Tty": true,
               "OpenStdin": true,
               "StdinOnce": false,
               "Env": [
                   "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                   "NGINX_VERSION=1.13.12"
               ],
               "Cmd": [
                   "nginx",
                   "-g",
                   "daemon off;"
               ],
               "ArgsEscaped": true,
               "Image": "nginx:alpine",
               "Volumes": null,
               "WorkingDir": "",
               "Entrypoint": null,
               "OnBuild": null,
               "Labels": {
                   "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
               },
               "StopSignal": "SIGTERM"
           },
           "NetworkSettings": {
               "Bridge": "",
               "SandboxID": "feb9d9634faebe9a614daebde47baa2b7f4bb2a251c1a34d8110d00aeaa0ae22",
               "HairpinMode": false,
               "LinkLocalIPv6Address": "",
               "LinkLocalIPv6PrefixLen": 0,
               "Ports": {
                   "80/tcp": [
                       {
                           "HostIp": "0.0.0.0",
                           "HostPort": "8000"
                       }
                   ]
               },
               "SandboxKey": "/var/run/docker/netns/feb9d9634fae",
               "SecondaryIPAddresses": null,
               "SecondaryIPv6Addresses": null,
               "EndpointID": "6391749f48f81bead415550f29e0fccd9a1d7b8ab1c315e99b8eda42680d65ff",
               "Gateway": "172.17.0.1",
               "GlobalIPv6Address": "",
               "GlobalIPv6PrefixLen": 0,
               "IPAddress": "172.17.0.2",
               "IPPrefixLen": 16,
               "IPv6Gateway": "",
               "MacAddress": "02:42:ac:11:00:02",
               "Networks": {
                   "bridge": {
                       "IPAMConfig": null,
                       "Links": null,
                       "Aliases": null,
                       "NetworkID": "edc65f4ec2c6e3ef4cc334751b7d979374a97011b103815b3e0bb237a8b6b8c0",
                       "EndpointID": "6391749f48f81bead415550f29e0fccd9a1d7b8ab1c315e99b8eda42680d65ff",
                       "Gateway": "172.17.0.1",
                       "IPAddress": "172.17.0.2",
                       "IPPrefixLen": 16,
                       "IPv6Gateway": "",
                       "GlobalIPv6Address": "",
                       "GlobalIPv6PrefixLen": 0,
                       "MacAddress": "02:42:ac:11:00:02",
                       "DriverOpts": null
                   }
               }
           }
       }
   ]

Zobraz detailní informace o kontejnerech::

   $ docker inspect python-test python:3-alpine

.. note::

   Inspekci lze aplikovat i na jakéoliv další Docker objekty, tj. i obrazy::

      $ docker inspect alpine

inspect -f
""""""""""

Zobraz zdrojový obraz kontejneru::

   $ docker inspect -f '{{.Config.Image}}' nginx
   nginx:alpine

Zobraz IP adresu kontejneru::

   $ docker inspect -f '{{.NetworkSettings.IPAddress}}' nginx
   172.17.0.2

Zobraz namapované porty kontejneru::

   $ docker inspect -f '{{range $p, $conf := .NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' nginx
    80/tcp -> 8000

Zobraz volumy kontejneru::

   $ docker inspect -f '{{range .Mounts }} {{.Source}} {{end}}' nginx
   /var/lib/docker/volumes/3349e238e567d0b51aa287d88790248f7978a2d79ba1e481b142be6f6ff78207/_data

rename
^^^^^^

Přejmenuj kontejner na nový název::

   $ docker rename nginx nginx-new

.. note::

   Přejmenovat lze jak běžící, tak i neběžící kontejner.

update
^^^^^^

update --restart
""""""""""""""""

Updatuj restartovací politiku pro daný kontejner::

   $ docker update --restart no python-test

Updatuj restartovací politiku pro dané kontejnery::

   $ docker update --restart no python-test python-test-test

diff
^^^^

Zobraz změny v souborovém systému od začátku běhu kontejneru::

   $ docker diff nginx
   C /lib/apk/db/lock
   C /root
   A /root/.ash_history
   C /run
   A /run/nginx.pid
   C /tmp
   C /var/cache/nginx
   D /var/cache/nginx/client_temp
   D /var/cache/nginx/fastcgi_temp
   D /var/cache/nginx/proxy_temp
   D /var/cache/nginx/scgi_temp
   D /var/cache/nginx/uwsgi_temp

.. note::

   Význam jednotlivých písmen:

   * ``A``

     * přidán nový soubor nebo adresář

   * ``C``

     * změněn soubor nebo adresář

   * ``D``

     * smazán soubor nebo adresář

cp
^^

Zkopíruj soubory nebo adresáře z lokálního adresáře do kontejneru::

   $ docker cp Dockerfile nginx:/
   $ docker cp Dockerfile nginx:/davie/
   no such directory

Zkopíruj soubory nebo adresáře z kontejneru do lokálního adresáře::

   $ docker cp nginx:/Dockerfile Daviefile
   $ docker cp nginx:/Dockerfile davie/Daviefile
   no such directory

.. note::

   Kontejner musí běžet nebo být alespoň pozastaven.

exec
^^^^

Spusť příkaz v běžícím kontejneru::

   $ docker exec nginx ps -a
   PID   USER     TIME   COMMAND
       1 root       0:00 nginx: master process nginx -g daemon off;
       7 nginx      0:00 nginx: worker process
      39 root       0:00 ps -a

.. note::

   Spuštění příkazu selže, pokud je kontejner běžící, ale procesy v něm
   pozastavený::

      $ docker exec nginx ps -a
      Error response from daemon: Container nginx is paused, unpause the container before exec

exec -d
"""""""

Spusť příkaz na pozadí v běžícím kontejneru::

   $ docker exec -d nginx touch /tmp/test

exec -e
"""""""

Spusť příkaz s danou proměnnou v běžícím kontejneru::

   $ echo $TEST

   $ docker exec -e TEST=test nginx echo $TEST

   $ docker exec -e TEST=test nginx sh -c 'echo $TEST'
   test

.. note::

   Někdy příkazy nemusí fungovat, proto je vhodné je spustit jako příkaz
   v shellu pomocí příkazu ``sh -c "echo $TEST"``, případně v bashi, pokud
   existuje, jako ``/bin/bash -c 'echo $TEST'``.

exec -it
""""""""

Spusť v interaktivním módu shell v běžícím kontejneru::

   $ docker exec -it nginx sh
   / # pwd
   /
   / # whoami
   root

.. note::

   Shell, bash nebo i ostatní příkazy nemusí v kontejneru vůbec existovat::

      $ docker exec -it nginx bash
      OCI runtime exec failed: exec failed: container_linux.go:348: starting container process caused "exec: \"bash\": executable file not found in $PATH": unknown

.. tip::

   Pokud je příkaz spuštěn v interaktivním režimu, tak výstupy příkazů mohou
   být obarveny na rozdíl od varianty bez interaktivního režimu::

      $ docker exec nginx ls -l
      $ docker exec -it nginx ls -l

exec -u
"""""""

Spusť příkaz jako konkrétní uživatel v běžícím kontejneru::

   $ docker exec -u davie nginx ls /

.. note::

   Daný uživatel musí existovat v kontejneru. Defaultně je použit ``root``
   uživatel, ať už při buildování obrazu nebo běhu kontejneru, který má
   mimojiné přístup ke kernelu hosta, kde běží Docker.

exec -w
"""""""

Spusť příkaz v daném pracovním adresáři v běžícím kontejneru::

   $ docker exec nginx pwd
   /
   $ docker exec -w /tmp nginx pwd
   /tmp

logs
^^^^

Zobraz jednorázově logy z běžícího kontejneru::

   $ docker logs nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

logs -f
"""""""

Zobraz nepřetržitě logy z běžícího kontejneru::

   $ docker logs -f nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   ^C

.. note::

   Nepřetržitý výpis logu lze klasicky ukončit pomocí klávesové zkratky
   ``CTRL + c ``, aniž by se kontejner ukončil.

logs --since
""""""""""""

Zobraz jednorázově logy z běžícího kontejneru od konkrétního času doteď::

   $ docker logs --since 2018-06-02 nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   $ docker logs --since 2018-06-02T09:00:00 nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

.. note::

   Čas v kontejnerech nemusí sedět s časem počítače kvůli časové zóně. Při
   filtrování času se automaticky zohledněju časová ona počítače, není-li
   nastaveno jinak::

      $ docker logs --since 2018-06-02T09:00:00Z  # UTC
      $ docker logs --since 2018-06-02T09:00:00+01:00 # UTC + 1 hour
      $ docker logs --since 2018-06-02T09:00:00-01:00 # UTC - 1 hour

.. tip::

   Pro hodiny, minuty a sekundy lze použít relativní čas::

      $ docker logs --since 1h30m15s nginx
      172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
      172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
      172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

logs --tail
"""""""""""

Zobraz posledních N rádků logů z běžícího kontejneru::

   $ docker logs nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   $ docker logs --tail 1 nginx
   172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

logs --until
""""""""""""

Zobraz jednorázově logy z běžícího kontejneru do konkrétního času::

   $ docker logs --until 2018-06-02T11:11:11 nginx
   172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
   172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

.. note::

   Stejně jako u volby ``--until`` se automaticky zohledňuje časová zóna.

.. tip::

   Ve spojení s volbou ``--since`` lze vytvořit time range od do::

      $ docker logs --since 2018-06-02T00:00:00 --until 2018-06-02T12:00:00 nginx
      172.17.0.1 - - [02/Jun/2018:09:05:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
      172.17.0.1 - - [02/Jun/2018:09:09:46 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"
      172.17.0.1 - - [02/Jun/2018:09:09:47 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" "-"

pause
^^^^^

Pozastav běžící procesy v běžícím kontejneru::

   $ docker pause nginx
   nginx
   $ docker ps
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                   PORTS                  NAMES
   ef45ce5483dc        nginx:alpine        "nginx -g 'daemon of…"   42 minutes ago      Up 31 seconds (Paused)   0.0.0.0:8000->80/tcp   nginx

Pozastav běžící procesy v běžících kontejnerech::

   $ docker pause one two three

unpause
^^^^^^^

Rozeběhni pozastavené procesy v běžícím kontejneru::

   $ docker unpause nginx
   nginx

Rozeběhni pozastavené procesy v běžících kontejnerech::

   $ docker unpause one two three

stop
^^^^

Ukonči šetrně běžící kontejner podle id::

   $ docker stop d506a2c71fd0

Ukonči šetrně běžící kontejner podle jména::

   $ docker stop test

Ukonči šetrně několik kontejnerů::

   $ docker stop one two three

Ukonči šetrně všechny běžící kontejnery::

   $ docker stop $(docker ps -f 'status=running')

.. note::

   Šetrné ukončení kontejneru trvá o něco déle, než násilná varianta. Defaultně
   se běžícíc kontejner pozastaví nejpozději do 10 sekund.

restart
^^^^^^^

Ukonči šetrně běžící kontejner podle id a opět jej nastartuj::

   $ docker restart d506a2c71fd0

Ukonči šetrně běžící kontejner podle jména a opět jej nastartuj::

   $ docker restart test

Ukonči šetrně několik kontejnerů a opět je nastartuj::

   $ docker restart one two three

Ukonči šetrně všechny běžící kontejnery a opět je nastartuj::

   $ docker restart $(docker ps -f 'status=running')

.. note::

   Pomocí restartu nebo startu lze znovu spustit ukončený kontejner.

kill
^^^^

Ukonči násilně běžící kontejner podle ID::

   $ docker kill d506a2c71fd0

Ukonči násilně běžící kontejner podle jména::

   $ docker kill test

Ukonči násilně několik kontejnerů::

   $ docker kill one two three

Ukonči násilně všechny běžící kontejnery::

   $ docker kill $(docker ps -f 'status=running')

rm
^^

Odstraň neběžící kontejner podle ID::

   $ docker rm 847e7641783c
   847e7641783c

Odstraň neběžící kontejner podle náhodně vygenerovaného jména::

   $ docker rm cocky_brahmagupta
   cocky_brahmagupta

Odstraň neběžící kontejner podle nastaveného jména::

   $ docker rm test
   test

Odstraň několik neběžících kontejnerů::

   $ docker rm one two three

Odstraň všechny neběžící kontejnery::

   $ docker rm $(docker ps -aq)
   59b0da7f56b0
   c75bab6a06e3
   Error response from daemon: You cannot remove a running container 5f9efb75022d7a0cb241ebb6aed39dd032b3a7d19c1a05775b15ae84fb031839. Stop the container before attempting removal or force remove

.. note::

   Při smazání všechn neběžících kontejnerů se běžící kontejnery budou
   ignorovat.

rm -f
"""""

Odstraň násilně běžící kontejner(y)::

   $ docker rm nginx
   Error response from daemon: You cannot remove a running container 847e7641783cd884578e39515303a90a8a16713a1c8faea8c9cf5163feaf4d5c. Stop the container before attempting removal or force remove
   $ docker rm -f nginx
   nginx

Odstraň násilně několik kontejnerů::

   $ docker rm -f one two three

Odstrań všechny běžíí i neběžící kontejnery::

   $ docker rm -f $(docker ps -aq)

rm -v
"""""

Odstraň neběžící kontejner včetně jeho volume::

volume
^^^^^^

ls
""

Zobraz všechny volumy::

   $ docker volume ls
   DRIVER              VOLUME NAME
   local               25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f
   local               63372f208f08c1cc8857b7145eaa6186770dfd956023cade9e4e332cdc7b5b6e
   local               data

Zobraz všechny volumy podle jejich ID::

   $ docker volume ls -q
   25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f
   63372f208f08c1cc8857b7145eaa6186770dfd956023cade9e4e332cdc7b5b6e
   data

Zobraz jen nepoužité dangling volumy::

   $ docker volume ls -f 'dangling=true'
   DRIVER              VOLUME NAME
   local               ea5a9d4c6085cbd88bdb84c41a50c0a14323eb474d5ddb01d99aca1353509744

.. note::

   Dangling volumy je třeba taktéž pravidelně mazat, neboť nepatří k žádnému
   existujícimu kontejneru a tudíž opět zabírají místo na disku.

inspect
"""""""

Zobraz detailní informace o volume::

   $ docker volume inspect 25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f
   [
       {
           "CreatedAt": "2018-06-04T22:51:19+02:00",
           "Driver": "local",
           "Labels": null,
           "Mountpoint": "/var/lib/docker/volumes/25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f/_data",
           "Name": "25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f",
           "Options": null,
           "Scope": "local"
       }
   ]

Zobraz detailní informace o všech volumech::

   $ docker volume inspect $(docker volume ls -q)

Zobraz namontované místo daného volumu na disku::

   $ docker volume inspect -f '{{ .Mountpoint }} ' 25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f
   /var/lib/docker/volumes/25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f/_data

.. note::

   V namontovaném místu na disku lze změnit obsah volumu, přičemž tato změna se
   projeví i v běžícím kontejneru, avšak je třeba mít patričné oprávnění::

      $ sudo -s  # root non-login shell
      $ cd $(docker volume inspect -f '{{ .Mountpoint }}' 3349e238e567d0b51aa287d88790248f7978a2d79ba1e481b142be6f6ff78207)
      $ touch test.txt
      $ exit

rm
""

Smaž volume, který se nepoužívá::

   $ docker volume rm ea5a9d4c6085cbd88bdb84c41a50c0a14323eb474d5ddb01d99aca1353509744
   ea5a9d4c6085cbd88bdb84c41a50c0a14323eb474d5ddb01d99aca1353509744

Smaž násilně volume, který se používá::

   $ docker volume rm 25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f
   Error response from daemon: unable to remove volume: remove 25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f: volume is in use - [dcec802018bc54bfafc5d4f6504bcca009c4a24c3ea9250a88fa60d8b2c96d01]
   $ docker volume rm -f 25e173d0546ceac9764988d74c6b30e9cd4b13b22ffbce1d9d6fd2977469e08f

Smaž všechny danling volumy::

   $ docker volume rm $(docker volume ls -f 'dangling=true' -q)

prune
"""""

Smaž všechny nepoužité volumy::

   $ docker volume prune
   WARNING! This will remove all local volumes not used by at least one container.
   Are you sure you want to continue? [y/N]

Smaž všechny nepoužité volumy bez nutnosti potvrzení::

   $ docker volume prune -f

system
^^^^^^

prune
"""""

Smaž všechny dangling obrazy, kontejnery, volumy a nastavené sítě::

   $ docker system prune
   WARNING! This will remove:
           1. all stopped containers
           2. all networks not used by at least one container
           3. all dangling images
           4. all build cache
   Are you sure you want to continue? [y/N]

Smaž všechny dangling objekty včetně nepouživaných obrazů a volume::

   $ docker system prune -av

.. note::

   ``Prune`` subpříkaz existuje i u obrazů či kontejnerů včetně volby ``-f``
   pro přeskočení potvrzení::

      $ docker image prune  # remove dangling images
      $ docker image prune -f  # force remove dangling images
      $ docker image prune -a  # remove dangling images including unused images
      $ docker image prune -af  # force remove dangling images including unused images
      $ docker container prune  # remove stopped containers
      $ docker container prune -f  # force remove stopped containers
