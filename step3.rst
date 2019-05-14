.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


*Building a container from a Dockerfile*
----------------------------------------

One of the most important aspects of Docker is that everything in the container
can be neatly documented in a |Dockerfile| - a plain text document specifying
the steps used to build the container. Let's build a container that will run
|fastqc| a popular bioinformatics tool to check the quality of DNA sequencing
reads.


First, we will try to install fastqc on the ubuntu image just as if we were
installing it on an ordinary ubuntu machine:

  1. Open a bash session on an ubuntu container

    .. code:: Bash

      docker run -it ubuntu bash

  2. Next we will download and unzip the fastqc program

    .. code:: Bash

      wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.8.zip

    Unfortunately we get the following error

    .. code:: Bash

      bash: wget: command not found

    This is because the containerized version of Ubuntu really is a minimal set
    of tools. Many small tools you expect to be on the container will need to be
    installed.

  3. Let's install `wget`, `unzip`, and a few other dependancies

    .. code:: Bash

      # update the package list
      apt-get update

      # install the needed packages including java and a perl library which we
      # need for fastqc
      apt-get install wget unzip default-jdk libfindbin-libs-perl

  4. Now let's attempt to install fastqc

    .. code:: Bash

      wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.8.zip
      unzip fastqc_v0.11.8.zip

  5. Let's configure fastqc and then test on some sample data

    .. code:: Bash

      # make fastqc executable
      chmod 755 /FastQC/fastqc

      # add fastqc to the system path by linking to /bin
      ln -s /FastQC/fastqc /bin

      # get some sample data
      wget https://de.cyverse.org/dl/d/48CAB430-473B-4853-AABE-1845A83204C7/small.fastq

      #run FastQC
      fastqc small.fastq



Now that we know fastqc works, we can record the steps we went through in a
Dockerfile. Currently, when we exit the container we have been working
interactively in (in the bash shell) all of our work will be lost. Creating a
Dockefile will allow us to build a new container image with all of our
configuration saved.

  .. tip::

     A |Dockerfile| is a textfile and has a simple format

     .. code:: text

       # Comment

         INSTRUCTION arguments

     Comments start with a "#" and instructions start with one of a few basic
     commands. Some of the most important are:

     - **FROM**: Describes an existing Docker image to start building from. You
       can start from 'scratch', but will usually start from a basic image like
       the Ubuntu machine we have used above.
     - **RUN**: Runs a command as you would at the shell. This creates a Docker
       layer in the image (See |Dockerfile| instructions for more on this).
     - **LABLE**: Allows you to add metadata to your image in a "key=value" format.
     - **EXPOSE**: Indicates specific ports to be listened to.
     - **ENV**: Allows you to set environment variables.
     - **ADD**: Allows you to copy files into the container when it is built
     - **COPY**: Allows you to copy files into the contain when it is built (See
       |Dockerfile| for the subtle differences between ADD and COPY behavior).
     - **ENTRYPOINT**: Specifies a specific application to run when the container is
       run. See also |Dockerfile| for the differences between this and a similar
       instruction "CMD".

We can create a Dockerile using the nano text editor. Notice the comments in
the text, there are some specific ways you will want to run commands in the
Dockerfile

  6. Open a text editor (outside of the container) and create a Dockerfile. We
  will do this in an empty directory.

    .. code:: Bash

      mkdir dockerfile
      cd dockerfile
      nano Dockerfile

  7. Copy or write the following

    .. code:: text

        # Build this container from the official Ubuntu Image
        # Make sure to use a tag that specifies version
        # i.e. ubuntu:bionic-20181112 not just ubuntu
        # The first line of your Dockerfile must be a FROM instruction
        FROM ubuntu:bionic-20181112

        # Add some metadata to describe our container
        LABEL maintainer="yourname"
        LABEL maintainer_email="youremail"
        LABEL version="1.0"

        # The ADD command will fetch and unzip the fastqc software
        ADD https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.8.zip /

        # We will run some commands just as we did in bash
        # Notice that we use the -y option for our apt-get since we can't say y during the build process
        # We also want to run the apt-get update in the same line as our install
        # We connect those commands with && to specify that the first command must exit
        # successfully before the second command is executed
        # We won't install wget since the ADD command eliminates the need

        RUN apt-get update -y && apt-get install -y\
         default-jdk\
         libfindbin-libs-perl\
         unzip

        # We will modify the permission on the software and create our symbolic link

        RUN unzip /fastqc_v0.11.8.zip && chmod 755 /FastQC/fastqc && ln -s /FastQC/fastqc /bin

        # We will define fastqc as the application to run when this container starts
        ENTRYPOINT ["fastqc"]

  8. Next, we will build our container with the following command


    .. code:: Bash

      docker build -t fastqc:1.0 .

  9. After the build is completed we should see our container in the list of
  Docker images on our machine

    .. code:: Bash

      docker images

      REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
      fastqc              1.0                 0ab4e3a50edc        3 minutes ago       774MB


  10. Finally, we can use our fastqc machine on data. Download the data on your
  host machine, and then use the created Docker image as if it were an
  application

    .. code:: Bash

      mkdir ~/data
      cd ~/data
      wget https://de.cyverse.org/dl/d/48CAB430-473B-4853-AABE-1845A83204C7/small.fastq

      # we use the -v flag to mount our ~/data directory to /data (which will be
      # created when this command is run). We then specify the file for the
      # fastqc program to run on.

      docker run -v ~/data:/data fastqc:1.0 /data/small.fastq

  You should now have two outputs in your `~/data` directory `small_fastqc.html`
  and `small_fastqc.zip`.

*Summary*
~~~~~~~~~~~

A Dockerfile allows you to transparently document all the dependancies and steps
needed to describe a software tool. You can then run this tool as a Docker
container for full reproducibility.

**Next Steps:**

----------

 - Learn about |pushing your Docker image to Dockerhub|
 - Create a GitHub repository to manage your dockerfiles
 - Learn more about |Best practices for writing Dockerfiles|
 - Learn |more about Docker|


----------

Additional information, help
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
    Short description and links to any reading materials

Search for an answer:
|CyVerse Learning Center| or
|CyVerse Wiki|

Post your question to the user forum:
|Ask CyVerse|

----

**Fix or improve this documentation**

- On Github: |Github Repo Link|
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

.. |Dockerfile|  raw:: html

   <a href="https://docs.docker.com/engine/reference/builder/" target="blank">Dockerfile</a>

.. |fastqc| raw:: html

   <a href="https://www.bioinformatics.babraham.ac.uk/projects/fastqc/" target="blank">fastqc</a>

.. |pushing your Docker image to Dockerhub| raw:: html

   <a href="https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html" target="blank">pushing your Docker image to Dockerhub</a>

.. |Best practices for writing Dockerfiles| raw:: html

   <a href="https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#dont-install-unnecessary-packages" target="blank">Best practices for writing Dockerfiles</a>

.. |more about Docker| raw:: html

   <a href="https://docs.docker.com/get-started/" target="blank">more about Docker</a>
