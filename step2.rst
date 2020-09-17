.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


*Pulling and running a container from Docker Hub*
-------------------------------------------------

After installing Docker, you can verify your installation by running a container
from |Docker Hub|. Docker Hub is service that allows you to store and share
containers. When building your own container, you will usually start from a
a pre-existing container. For example, the |Ubuntu Docker| page on Docker Hub hosts
official Ubuntu operating system containers. These are minimal installations
of Ubuntu you can customize to build a new container, without installing an
operating system.

  .. tip::

      Docker Hub hosts |Official Images|, which are generally more secure than
      unverified images (anyone with a Docker Hub account can host and image).
      Official images are also more likely to be configured correctly.

We will test your installation by pulling and running the "Hello World" image:

  1. Run the following command:

    .. code:: Bash

      docker run hello-world

   You will get the following output if Docker is installed and configured successfully:

    .. code:: Bash

     Unable to find image 'hello-world:latest' locally
     latest: Pulling from library/hello-world
     1b930d010525: Pull complete
     Digest: sha256:5f179596a7335398b805f036f7e8561b6f0e32cd30a32f5e19d17a3cda6cc33d
     Status: Downloaded newer image for hello-world:latest

     Hello from Docker!
     This message shows that your installation appears to be working correctly.

     To generate this message, Docker took the following steps:
      1. The Docker client contacted the Docker daemon.
      2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
         (amd64)
      3. The Docker daemon created a new container from that image which runs the
         executable that produces the output you are currently reading.
      4. The Docker daemon streamed that output to the Docker client, which sent it
         to your terminal.

     To try something more ambitious, you can run an Ubuntu container with:
      $ docker run -it ubuntu bash

     Share images, automate workflows, and more with a free Docker ID:
      https://hub.docker.com/

     For more examples and ideas, visit:
      https://docs.docker.com/get-started/

  2. As suggested, we can run an instance of Ubuntu using the following command.
     Notice, we explicitly retrieve the container, use the `-it` (interactive) option
     and start the bash shell within the container:

    .. code:: Bash

      docker run -it ubuntu bash

    Try a few commands; you can use the `exit` command to exit the container.

  3. You can see a list of container images you have downloaded to your computer
     using the `info` command:

    .. code:: Bash

      docker images

    .. code:: Bash

      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      ubuntu              latest              d131e0fa2585        2 weeks ago         102MB
      hello-world         latest              fce289e99eb9        4 months ago        1.84kB

  4. You can see the status of your containers using the using the `ps` command:

    .. code:: Bash

      docker ps

      CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

    In this case, no containers are running.

  5. Let's try a more complex container - using this command we will pull a
     container running RStudio

     .. code:: Bash

       docker run -e PASSWORD=<YOUR_PASS> -p 8787:8787 rocker/rstudio

       # -e passes an environment variable - change <YOUR_PASS>, e.g. 12345
       # -p maps a port inside the docker container to one on the host machine

    You will now have an RStudio instance running at port 8787 of your computer.
    To access open a web browser and go to your machine's IP address + ":8787" \
    (this will generally be 127.0.0.1:8787). Username will be "rstudio" and
    password will be whatever you chose in the command above


  .. Tip::

     A full list of Docker commands and their explanation can be found here:
     |Docker child commands|. 

----

**Fix or improve this documentation**

- Search for an answer:
  |CyVerse Learning Center|
- Ask us for help:
  click |Intercom| on the lower right-hand side of the page
- Report an issue or submit a change:
  |Github Repo Link|
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_



----

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


.. Comment: Place Images Below This Line
   use :width: to give a desired width for your image
   use :height: to give a desired height for your image
   replace the image name/location and URL if hyperlinked


 .. |Clickable hyperlinked image| image:: ./img/IMAGENAME.png
    :width: 500
    :height: 100
 .. _CyVerse logo: http://learning.cyverse.org/

 .. |Static image| image:: ./img/IMAGENAME.png
    :width: 25
    :height: 25



.. Comment: Place URLS Below This Line

   # Use this example to ensure that links open in new tabs, avoiding
   # forcing users to leave the document, and making it easy to update links
   # In a single place in this document

   .. |Substitution| raw:: html # Place this anywhere in the text you want a hyperlink

      <a href="REPLACE_THIS_WITH_URL" target="blank">Replace_with_text</a>


.. |Github Repo Link|  raw:: html

   <a href="https://github.com/CyVerse-learning-materials/creating-docker-containers-quickstart" target="blank">Github Repo Link</a>

.. |Docker Hub| raw:: html

   <a href="https://hub.docker.com/" target="blank">Docker Hub</a>

.. |Ubuntu Docker| raw:: html

   <a href="https://hub.docker.com/_/ubuntu" target="blank">Ubuntu Docker</a>

.. |Official Images| raw:: html

   <a href="https://docs.docker.com/docker-hub/official_images/" target="blank">Official Images</a>

.. |Docker child commands| raw:: html

   <a href="https://docs.docker.com/v17.12/edge/engine/reference/commandline/docker/" target="blank">Docker child commands</a>
