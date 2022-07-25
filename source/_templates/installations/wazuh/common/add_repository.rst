.. Copyright (C) 2015, Wazuh, Inc.

.. tabs::

   .. group-tab:: Yum

      #. Import the GPG key:

         .. code-block:: console

            # rpm --import https://packages.wazuh.com/key/GPG-KEY-WAZUH

      #. Add the repository:

         .. code-block:: console

            # cat > /etc/yum.repos.d/wazuh.repo << EOF
            [wazuh]
            gpgcheck=1
            gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
            enabled=1
            name=EL-\$releasever - Wazuh
            baseurl=https://packages.wazuh.com/4.x/yum/
            protect=1
            EOF

   .. group-tab:: APT - Debian 10.x (Buster) / Ubuntu 18.04 (Bionic Beaver) or earlier

      #. Install the GPG key:

         .. code-block:: console

            # curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add -

      #. Add the repository:

         .. code-block:: console

            # echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list

      #. Update the package information:

         .. code-block:: console

            # apt-get update


      
.. End of include file
