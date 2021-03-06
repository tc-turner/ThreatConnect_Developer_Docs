Delete IP Addresses
^^^^^^^^^^^^^^^^^^^

The example below demonstrates how to delete an Address Indicator from the ThreatConnect platform:

.. code-block:: python
    :linenos:
    :emphasize-lines: 23-24

    ...

    tc = ThreatConnect(api_access_id, api_secret_key, api_default_org, api_base_url)

    # instantiate an Indicators container
    indicators = tc.indicators()

    owner = 'Example Community'

    # specify a specific address in a specific owner (in this case '8.8.8.8' in the 'Example Community')
    filter1 = indicators.add_filter()
    filter1.add_owner(owner)
    filter1.add_indicator('8.8.8.8')

    # retrieve the Indicator
    indicators.retrieve()

    # prove that there is only one Indicator retrieved
    assert len(indicators) == 1

    try:
        for indicator in indicators:
            # delete the Indicator
            indicator.delete()
    except RuntimeError as e:
        print('Error: {0}'.format(e))
        sys.exit(1)

.. note:: In the prior example, no API calls are made until the ``delete()`` method is invoked.
