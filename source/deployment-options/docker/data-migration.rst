.. Copyright (C) 2015, Wazuh, Inc.

.. meta::
   :description: How to migrate data from Wazuh 4.2 with Open Distro to Wazuh Indexer in Docker production deployments.

Open Distro data migration to Wazuh indexer on Docker
=====================================================

For users using Wazuh version 4.2.x with Open Distro for Elasticsearch. This procedure explains how to migrate data from Open Distro for Elasticsearch to Wazuh Indexer in Docker production deployments (v4.2.x to v|WAZUH_LATEST_MINOR|).

Assuming that version 4.2.x production cluster was previously deployed.

#. From the ``wazuh-docker`` directory, stop the current v4.2.x environment:

   .. code-block:: console

      # docker-compose -f production-cluster.yml stop

#. Check that Elasticsearch volumes are present: 

   .. code-block:: console

      # docker volume ls --filter name='wazuh-docker_elastic-data'

#. Inspect Elasticsearch volumes and save the **com.docker.compose.version** value to be used in step 7: 

   .. code-block:: console

      # docker volume inspect wazuh-docker_elastic-data-1

#. Take down the current v4.2.x environment:

   .. code-block:: console

      # docker-compose -f production-cluster.yml down

#. Exit the current ``wazuh-docker`` directory and rename it to ``wazuh-docker-4.2.X``.

#. Clone the Wazuh v|WAZUH_LATEST_MINOR| repository to your system:

   .. code-block:: console

      # git clone https://github.com/wazuh/wazuh-docker.git -b v|WAZUH_LATEST_DOCKER| --depth=1

#. Then enter into the ``multi-node`` directory, and run the ``volume-migrator`` script. This will create new volumes for v|WAZUH_LATEST_MINOR| and copy data from old volumes to the newly created volumes. The arguments are the Docker-compose version and project name, see an example below. This step can also be done manually, see steps 5 and 6 in Wazuh Docker `Github <https://github.com/wazuh/wazuh-docker/blob/|WAZUH_LATEST_MINOR|/multi-node/Migration-to-Wazuh-|WAZUH_LATEST_MINOR|.md>`__:

   .. code-block:: console

      # ./volume-migrator.sh 1.29.2 multi-node

#. Start the v|WAZUH_LATEST_MINOR| environment:

   .. code-block:: console

      # docker-compose -f generate-indexer-certs.yml run --rm generator
      # docker-compose up -d
