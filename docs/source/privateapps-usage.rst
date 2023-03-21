=========================
Examples for class: privateapps
=========================

The aim of this class is to provide simple object based access to the 
Netskope Private Apps API and make it as simple as possible to code given the available
swagger documentation. 


Basic Usage
-----------

For Netskope Private Apps therefore the basic usage structure for a *get* is::

    import netskope
    privateapps = netskope.privateapps(<ini file>)
    response = privateapps.get(<object path>)
    if response.status_code in b1ddi.return_codes_ok:
        print(response.text)
    else: 
        print(response.status_code)

With create and update the key difference is that a JSON body is supplied::

    payload = '{"app_name":"string","host":"string","real_host":"string","protocols":[{"type":"string","port":"string"}],"publishers":[{"publisher_id":"string","publisher_name":"string"}],"publisher_tags":[{"tag_name":"string"}],"tags":[{"tag_name":"string"}],"use_publisher_dns":true,"clientless_access":true,"trust_self_signed_certs":true}'
    response = privateapps.create('', body=payload)
    if repsonse.status_code in privateapps.return_codes_ok:
        print(repsonse.text)
    else: 
        print(response.status_code)
        print(response.text)

For a complete list of supported methods and details around parameters, 
please see the :doc:`class documentation </classes>`


Examples
--------

.. todo::
    These examples are placeholders, useful, but actual example set here is on 
    the todo.

.. code-block:: python

    # Note this is a set of rough examples to show method calls

    import netskope
    import logging

    log=logging.getLogger(__name__)
    # logging.basicConfig(level=logging.DEBUG)

    # Create a Netskope Private Application Object
    privateapps = netskope.privateapps()

    # Your can specify ini filename/path
    # privateapps = netskope.privateapps('/Users/<username/<path>/<inifile>')

    # Show API Key
    privateapps.api_key
    privateapps.api_version

    # Generic Get wrapper using "Swagger Path for object"
    # response = privateapps.get('<swagger path>')
    response = privateapps.get('/tags')
    
    # Response object handling
    response.status_code
    response.text
    response.json()

    # Get ID from key/value pair, Object Type is private_apps or tags, key can be app_name or host, value is the application name or the fqdn or ip from the app
    id = privateapps.get_id('', objecttype="private_apps", key="app_name", value="[Application Name]")
    # Example Result: '53