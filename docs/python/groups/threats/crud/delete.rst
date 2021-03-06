Delete Threats
^^^^^^^^^^^^^^

The example below demonstrates how to delete an Threat Resource in the
ThreatConnect platform:

.. code-block:: python
    :linenos:
    :emphasize-lines: 9-12,15-16

    ...

    tc = ThreatConnect(api_access_id, api_secret_key, api_default_org, api_base_url)

    # instantiate Threats container
    threats = tc.threats()

    owner = 'Example Community'
    # create an empty Threat
    threat = threats.add('', owner)
    # set the ID of the new Threat to the ID of the Threat you would like to delete
    threat.set_id(123456)

    try:
        # delete the Threat
        threat.delete()
    except RuntimeError as e:
        print(e)
        sys.exit(1)

.. note:: In the prior example, no API calls are made until the ``delete()`` method is invoked.

Code Highlights

+----------------------------------------------+-------------------------------------------------------------------+
| Snippet                                      | Description                                                       |
+==============================================+===================================================================+
| ``tc = ThreatConnect(api_access_id, api...`` | Instantiate the ThreatConnect object.                             |
+----------------------------------------------+-------------------------------------------------------------------+
| ``threats = tc.threats()``                   | Instantiate a Threats container object.                           |
+----------------------------------------------+-------------------------------------------------------------------+
| ``threat = threats.add('', owner)``          | Add a Resource object setting the name and Owner.                 |
+----------------------------------------------+-------------------------------------------------------------------+
| ``threat.set_id(20)``                        | Set the ID of the Threat to the **EXISTING** Threat ID to delete. |
+----------------------------------------------+-------------------------------------------------------------------+
| ``threat.delete()``                          | Trigger API calls to write all added, deleted, or modified data.  |
+----------------------------------------------+-------------------------------------------------------------------+
