
Quick Start
===========

First, :doc:`Install margaritashotgun <installing>`.

Capture A Single Machine
************************

A single machine can be captured using only the command line arguments for margaritashotgun.
First specify the server and user with the ``-s`` and ``-u`` flags respectively.
Next provide a path to an ssh key with ``-k`` (or use a password with the ``-p`` flag).
Finally provide a lime kernel module with ``-m`` and specify an output file with ``-f``

.. code-block:: bash

   margaritashotgun -s 172.16.20.10 -u root -k root_access.pem -m lime-3.13.0-74-generic.ko -f 172.16.20.10-mem.lime

Save Memory In S3
*****************

To save a file to s3 simply replace the ``-f`` or ``filename`` flags with ``-b`` or ``--bucket``.  Ensure that you have aws credentials configured prior to executing the following command.

.. code-block:: bash

   margaritashotgun -s 172.16.20.10 -u root -k root_access.pem -m lime-3.13.0-74-generic.ko -b memory_capture_bucket

Capture Multiple Machines
*************************

Run margaritashotgun with a configuration file like ``parallel_config.yml.example``

.. code-block:: bash

    aws:
        bucket: memory_dump_example
    hosts:
        - addr:     52.36.191.XXX
          port:     22
          username: ec2-user
          key:      access.pem
          module:   lime-4.1.19-24.31.amzn1.x86_64.ko
        - addr:     52.36.170.XXX
          port:     22
          username: ec2-user
          key:      access.pem
          module:   lime-4.1.19-24.31.amzn1.x86_64.ko
        - addr:     52.36.210.XXX
          port:     22
          username: ubuntu
          key:      dev.pem
          module:   lime-3.13.0-74-generic.ko
        - addr:     52.36.90.XXX
          port:     22
          username: ubuntu
          key:      dev.pem
          module:   lime-3.13.0-74-generic.ko
    workers: 2

.. note::

   In this example parallelism is limited to 2 workers.

Run the capture with:

.. code-block:: bash

   margaritashotgun -c your_custom_config.yml.
