Create Group Security Labels
""""""""""""""""""""""""""""

The code snippet below demonstrates how to add a security label to an Incident. This example assumes there is an Incident with an ID of ``123456``. To test this code snippet, change the ``incident_id`` variable to the ID of an incident in your owner. This same process also applies to all group types. Simply change ``tc.incidents()`` to the group type you would like to retrieve. The available group types are: ``tc.<adversaries|campaigns|documents|emails|incidents|signatures|threats>()``. This snippet also assumes that the target owner has a 'TLP Green' security label (security labels are not case sensitive when using the Python SDK).

.. code-block:: python
    :linenos:
    :emphasize-lines: 24-25

    ...

    tc = ThreatConnect(api_access_id, api_secret_key, api_default_org, api_base_url)

    # define the ID of the Incident we would like to retrieve
    incident_id = 123456

    # create an Incidents object
    incidents = tc.incidents()

    # set a filter to retrieve the Incident with the id: 123456
    filter1 = incidents.add_filter()
    filter1.add_id(incident_id)

    try:
        incidents.retrieve()
    except RuntimeError as e:
        print('Error: {0}'.format(e))
        sys.exit(1)

    for incident in incidents:
        print(incident.name)

        # add the 'TLP Green' label to the Incident
        incident.add_security_label('TLP Green')

        # commit the Incident with the new security label to ThreatConnect
        incident.commit()

.. note:: In the prior example, no API calls are made until the ``commit()`` method is invoked.
