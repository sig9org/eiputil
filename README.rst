.. image:: https://img.shields.io/pypi/v/eiputil.svg
 :target: https://pypi.org/project/eiputil/
.. image:: https://img.shields.io/pypi/l/eiputil.svg
 :target: https://pypi.org/project/eiputil/
.. image:: https://img.shields.io/pypi/pyversions/eiputil.svg
 :target: https://pypi.org/project/eiputil/
.. image:: https://img.shields.io/github/contributors/sig9org/eiputil.svg
 :target: https://github.com/sig9org/eiputil/graphs/contributors

eiputil
==================================================

A tool to help you operate AWS EC2 EIPs.

Usage
==================================================

.. code-block:: bash

    Usage: eiputil [OPTIONS] COMMAND [ARGS]...
    
      Shell completion for click-completion-command
    
      Available shell types:
    
        bash         Bourne again shell
        fish         Friendly interactive shell
        powershell   Windows PowerShell
        zsh          Z shell
    
      Default type: auto
    
    Options:
      --help  Show this message and exit.
    
    Commands:
      allocate       Allocate Elastic IP addresses.
      describe       Describe Elastic IP addresses.
      install        Install the click-completion-command completion.
      release        Release Elastic IP addresses.
      release-all    Release all Elastic IP addresses.
      show-ipranges  Show AWS ip-ranges.

Install the click-completion-command completion
==================================================

Install to use the tab completion function.

.. code-block:: bash

    $ eiputil install bash
    bash completion installed in /home/user/.bash_completion

Describe Elastic IP addresses.
==================================================

Displays a list of EIPs.

.. code-block:: bash

    $ eiputil describe
    {
      "IPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "InstanceId": "i-0123456789abcdefg",
          "AllocationId": "eipalloc-1110123456789abcd"
        },
        {
          "PublicIp": "192.0.2.2",
          "InstanceId": "",
          "AllocationId": "eipalloc-2220123456789abcd"
        }
      ]
    }

To display only addresses that are not associated with an instance, specify the --unassigned-only option.

.. code-block:: bash

    $ eiputil describe --unassigned-only
    {
      "IPAddresses": [
        {
          "PublicIp": "192.0.2.2",
          "InstanceId": "",
          "AllocationId": "eipalloc-2220123456789abcd"
        }
      ]
    }

Allocate Elastic IP addresses.
==================================================

Assign an EIP.

.. code-block:: bash

    $ eiputil allocate
    {
      "AllocatedIPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "AllocationId": "eipalloc-1110123456789abcd"
        }
      ]
    }

If you want to assign multiple EIPs, specify the number.

.. code-block:: bash

    $ eiputil allocate 3
    {
      "AllocatedIPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "AllocationId": "eipalloc-1110123456789abcd"
        },
        {
          "PublicIp": "192.0.2.2",
          "AllocationId": "eipalloc-2220123456789abcd"
        },
        {
          "PublicIp": "192.0.2.3",
          "AllocationId": "eipalloc-3330123456789abcd"
        }
      ]
    }

Release Elastic IP addresses.
==================================================

Release EIP.

.. code-block:: bash

    $ eiputil release 192.0.2.1
    {
      "ReleasedIPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "AllocationId": "eipalloc-1110123456789abcd"
        }
      ]
    }

If you want to release multiple EIPs, specify the EIPs consecutively.

.. code-block:: bash

    $ eiputil release 192.0.2.1 192.0.2.2
    {
      "ReleasedIPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "AllocationId": "eipalloc-1110123456789abcd"
        },
        {
          "PublicIp": "192.0.2.2",
          "AllocationId": "eipalloc-2220123456789abcd"
        }
      ]
    }

Release all Elastic IP addresses.
==================================================

Release all unassigned EIPs.

.. code-block:: bash

    $ eiputil release-all
    {
      "ReleasedIPAddresses": [
        {
          "PublicIp": "192.0.2.1",
          "AllocationId": "eipalloc-1110123456789abcd"
        },
        {
          "PublicIp": "192.0.2.2",
          "AllocationId": "eipalloc-2220123456789abcd"
        },
        {
          "PublicIp": "192.0.2.3",
          "AllocationId": "eipalloc-3330123456789abcd"
        }
      ]
    }

Show AWS ip-ranges.
==================================================

Show AWS ip-ranges.
(https://ip-ranges.amazonaws.com/ip-ranges.json)

.. code-block:: bash

    $ eiputil show-ipranges
    {
      "syncToken": "1582935190",
      "createDate": "2020-02-29-00-13-10",
      "prefixes": [
        {
          "ip_prefix": "13.248.118.0/24",
          "region": "eu-west-1",
          "service": "AMAZON"
        },
        {
          "ip_prefix": "18.208.0.0/13",
          "region": "us-east-1",
          "service": "AMAZON"
        },
            .
            .
            .
        {
          "ipv6_prefix": "2600:9000:ddd::/48",
          "region": "GLOBAL",
          "service": "CLOUDFRONT"
        },
        {
          "ipv6_prefix": "2600:9000:5300::/40",
          "region": "GLOBAL",
          "service": "CLOUDFRONT"
        }
      ]
    }
