==================
Usage and Examples
==================

Inifile configuration
---------------------

A sample inifile for the bloxone module is shared as *netskope.ini* and follows
the following format provided below::

    [Netskope]
    url = 'https://<tenant>.goskope.com'
    api_key = '<you API Key here>'

You can therefore simply add your API Key and personal management URL, and this is ready for the netskope
modules included.


Overview
--------

The aim of this module is to provide simple object based access to the 
Netskope APIs and make it as simple as possible to code given the available
swagger documentation. 

There are several classes/subclasses that provide this access. The base
class is :class:`nss`. This acts as a parent class for the Netskope Application
APIs.

The specific API 'trees' are then split in to subclasses of :class:`nss`:

    :class:`privateapps` 
        Access to the Netskope Private Apps API with core methods for *get*, *create*,
        *delete* and *update*.

Basic Usage
-----------

Using Netskope Private Apps as an example, the basic usage structure for a *get* is::

    import netskope
    privateapps = netskope.privateapps(<inifile>)
    response = privateapps.get(<object path>)
    if response.status_code in privateapps.return_codes_ok:
        print(response.text)
    else: 
        print(response.status_code)

Similarly for the other core functions, and classes. For details on method
specific parameters, please see the :doc:`class documentation </classes>`

For debugging purposes, the :mod:`netskope` module supports logging using 
:mod:`logging` using DEBUG.

.. warning::

    I have attempted to keep debugging clean, however, there is still potential
    for the debug output to produce full data dumps of API responses.


Generic API Wrapper
-------------------

It is also possible to use the netskope.nss class as a generic API wrapper with public methods
for *get*, *create*, *update* and *delete*. These can be used to pass a full URL, and where 
appropriate body and parameters. It is of course possible to build the URL using the attributes
of this class, in addition to manually entering the full url::

    import netskope
    nss = netskope.nss(<ini file>)
    url = 'https://<TENANT>.goskope.com/api/v2/steering/apps/private'
    response = nss.get(url)
    print(response.json())

    url = nss.privateapps_url + '/<Private Application ID>'
    response = nss.get(url)
    print(response.json())


Examples
--------

Although the basic flow of: instantiating the class with a configuration ini 
file; access the attributes or methods, with *get* almost being universal
as a method, and using the swagger object paths to access the required 
resource. Specific examples for each of the classes, and their use, is shown 
in more detail in the following documents:

.. toctree::
    :maxdepth: 4

    privateapps-usage

The remaining classes generally provide generic interfaces for *get*, *create*, *update* and *delete*.
Usage follows the same format of instantiating the class with an ini file and accessing the generic methods
using using the 'swagger' path for the appropriate object.

