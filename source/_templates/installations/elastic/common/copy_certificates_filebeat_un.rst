.. Copyright (C) 2022 Wazuh, Inc.

During the Elasticsearch installation, the ``certs.tar`` file was created. This guide assumes that a copy of this file has been placed in the root home folder (``~/``):

.. code-block:: console

  # tar -xf ~/certs.tar -C /etc/filebeat/certs/ ./filebeat.pem ./filebeat.key ./root-ca.pem

.. End of copy_certificates_filebeat.rst
