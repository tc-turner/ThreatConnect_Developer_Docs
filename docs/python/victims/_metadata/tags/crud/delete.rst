Delete Victim Tags
""""""""""""""""""

The code snippet below demonstrates how to delete a tag from a Victim. This example assumes there is a Victim with an ID of ``123456`` in the target owner. To test this code snippet, change the ``victim_id`` variable to the ID of a victim in your owner.

.. code-block:: python
    :linenos:

    ...

    tc = ThreatConnect(api_access_id, api_secret_key, api_default_org, api_base_url)

    # define the ID of the victim we would like to retrieve
    victim_id = 123456

    # create a victims object
    victims = tc.victims()

    # set a filter to retrieve the victim with the id: 123456
    filter1 = victims.add_filter()
    filter1.add_id(victim_id)

    try:
        victims.retrieve()
    except RuntimeError as e:
        print('Error: {0}'.format(e))
        sys.exit(1)

    for victim in victims:
        print(victim.name)

        # remove the 'Test' tag from the victim
        victim.delete_tag('Test')

        # commit the victim with the removed tag to ThreatConnect
        victim.commit()

.. note:: In the prior example, no API calls are made until the ``commit()`` method is invoked.
