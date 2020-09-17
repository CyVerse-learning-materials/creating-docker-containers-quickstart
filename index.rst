.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Creating and Running Docker Containers**
============================================

Goal
----

This is a short introduction to building a Docker container. Containers are
a starting point for applications within the CyVerse |Discovery Environment|,
including VICE applications (See: |VICE documentation|), or for applications
you may wish to deploy on |Atmosphere|. We will cover 1) setting up your
computer for Docker, 2) pulling and running a container from Docker Hub, and 3)
creating a Dockerfile.

----

.. toctree::
	:maxdepth: 2

	Setting up Docker on your computer <self>
	Pulling and running a container from Docker Hub <step2.rst>
	Building a container from a Dockerfile <step3.rst>


-----

Prerequisites
-------------

Downloads, access, and services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*In order to complete this tutorial you will need access to the following services/software*

 .. list-table::
   :header-rows: 1

   * - Prerequisite
     - Preparation/Notes
     - Link/Download
   * - Docker
     - You will need Docker CE installed on your machine complete this exercise
     - |Docker Setup|
   * - Docker Hub account
     - You will need a Docker Hub account to complete this exercise
     - |Docker Hub|
   * - CyVerse account
     - An account is not required but encouraged
     - |CyVerse User Portal|
   * - Atmosphere access
     - An account is not required unless you wish to complete exercises using a CyVerse virtual machine (Atmosphere)
     - |Atmosphere Manual|
   * - An active Atmosphere instance running Ubuntu
     - An account is not required unless you wish to complete exercises using a CyVerse virtual machine (Atmosphere)
     - |Ubuntu 18_04 GUI XFCE Base v2.0|

Platform(s)
~~~~~~~~~~~

*We will use the following CyVerse platform(s):*

.. list-table::
    :header-rows: 1

    * - Platform
      - Interface
      - Link
      - Platform Documentation
      - Quick Start
    * - Atmosphere
      - Command line (ssh) and/or Desktop (VNC)
      - |Atmosphere|
      - |Atmosphere Manual|
      - |Atmosphere Guide|

----

*Setting up Docker on your computer*
-------------------------------------
To get started, we need to install the "Docker daemon" - this is the software
which will allow us to run Docker containers. It is usually easily installed,
but since instructions may change we suggest you visit the |Docker Setup| website.
For more background about what Docker is, please see the |Docker get started|
website.

**If you are going to run Docker on your Mac/PC/Linux computer**

  1. Follow the instructions to install Docker: |Docker Setup|

**If you are going to run Docker on your on a CyVerse Atmosphere machine**

  1. Launch and connect via ssh to the |Ubuntu 18_04 GUI XFCE Base v2.0| image (
     see |Atmosphere Manual| for help launching and connecting)

    .. tip::

       If you are using Atmosphere, your `sudo` password is the same as your
       login credentials.

  2. Next, we need to install some dependancies to get Docker to run on our Ubuntu
     machine

    .. code:: Bash

      apt-get install -y  \
      apt-transport-https \
      ca-certificates \
      software-properties-common

  3. Next we will add a gpg key (so we can connect securely to the Docker repository)

    .. code:: Bash

      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

  4. Now we will add the Docker repository to the list of download sources

    .. code:: Bash

      add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"

  5. Next, we will update the repository lists

    .. code:: Bash

      sudo apt-get update

  6. Finally, we will install Docker

    .. code:: Bash

      sudo apt-get install -y docker-ce

----

Additional information, help
~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Post your question to the user forum:
|Ask CyVerse|

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
`Learning Center Home <http://learning.cyverse.org/>`__

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

.. |VICE documentation| raw:: html

   <a href="https://cyverse-visual-interactive-computing-environment.readthedocs-hosted.com/en/latest/index.html" target="blank">VICE documentation</a>

.. |Docker Setup| raw:: html

   <a href="https://docs.docker.com/install/" target="blank">Docker Setup</a>

.. |Docker Hub| raw:: html

   <a href="https://hub.docker.com/" target="blank">Docker Hub</a>

.. |Ubuntu 18_04 GUI XFCE Base v2.0| raw:: html

   <a href="https://atmo.cyverse.org/application/images/1556" target="blank">Ubuntu 18_04 GUI XFCE Base v2.0</a>

.. |Docker get started| raw:: html

   <a href="https://docs.docker.com/get-started/" target="blank">Docker get started</a>
