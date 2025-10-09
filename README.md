# 1Password Rest Collector IO
----

## About this Pack

This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the pack's context, eliminating the need to connect it to globally defined Sources and Destinations. 

This pack is designed to handle JSON data collected from the 1Password Audit Event API endpoint. The JSON is parsed and the timestamp normalized from the proper field within each event. The pack offers two different optional methods of reduction:

1. Drop, Sample, or Suppress based on action/object type. You can target individual action/object types by modifying the provided 1password_audit_events.csv lookup under Knowledge > Lookups.
2. Remove duplicate fields.

The pack also currently includes three forms of outputs:

1. Normalized JSON
2. OCSF - Primarily meant for Amazon Security Lake, the pack can normalize the data into the proper OCSF categories based on action/object type. The target OCSF category can also be managed on an individual action/object type basis through the lookup file `1password_audit_events.csv`.
3. Splunk - default index and sourcetype supplied from Knowledge > Variables, but can be overwritten in pipeline

## Deployment

* This pack is configured by default to use the Worker Group's *Default Destination*.
* To use the *Default Destination*: No changes are required. The pack will route the data to the destination currently set as the Default on the Worker Group.
* To use a different Destination: You must update the pack's routes to specify your desired Destination.
* For immediate functionality without requiring Pack route filter expression modifications, every bundled Source within this pack adds a hidden field: `__packsource`. This field allows for seamless routing based on the Pack source.

## Configure the Rest Collector Source

* Obtain a [Bearer Token](https://support.1password.com/events-reporting/#appendix-issue-or-revoke-bearer-tokens) from your 1Password Administrator.
* Enter the value for the Collect header field named `Authorization` in the following format: `'Bearer YOUR_BEARER_TOKEN'` (the value *must* be a valid JavaScript string)

## Configure Reductions and Output Format
* Data can be configured to output data in either OCSF or normalized JSON (Splunk) format - enable *only* one format!
* This pack includes several functions that can help reduce events. Please make sure you evaluate the functions before enabling, to ensure vital data is not missed.

### Configure your Destination/Update Pack Routes
To ensure proper data routing, you must make a choice: retain the current setting to use the Default Destination defined by your Worker Group, or define a new Destination directly inside this pack and adjust the pack's route accordingly.

### Commit and Deploy
Once everything is configured, perform a Commit & Deploy to enable data collection.

# Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.

## Release Notes

### Version 1.0.0
Initial release

## Contributing to the Pack

To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.

## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).