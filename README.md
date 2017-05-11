# Chef Audit Cookbook v3.1.0 Office Hour

## Deprecation Warnings
In order to make the audit cookbook easier to understand and consume, we have changed an important attribute
and the values that it accepts.

It is recommended that you modify your role or wrapper cookbooks to utilize these changes instead of the old as
they will no longer work in the next major version release of the cookbook.

`['audit']['collector']` has become `['audit']['reporter']`

Reporter is the attribute that controls where the inspec compliance report is targeted and ultimately how it is
sent to that location.

You may either pass `['audit']['reporter']` a string value for a single destination or an array of strings for
multiple destinations.

Possible values for `['audit']['reporter']`:
 - chef-compliance = report directly to Compliance Server
 - chef-automate = report directory to Automate (Note: If you were using `chef-visibilty` in the past, you must switch to this)
 - chef-server-compliance = report to Compliance Server via Chef Server
 - chef-server-automate = report to Automate via Chef Server (Note: If you were using `chef-server-visibilty` in the past, you must switch to this)
 - json-file = report to local file on filesystem in json format

## Supported Scenarios

The `['audit']['reporter']` should be used in conjunction with the `['audit']['fetcher']` when consuming profiles
via the Chef Server proxy. Using the Chef Server as a proxy for both reporting and fetching profiles is a
recommended approach as it is does not require any additional TCP/IP communication from clients to either the
Automate or Compliance servers.

With the Chef Server as the proxy, the communication path is: client<-->Chef Server<-->Automate / Compliance server
All communication between client and systems is over HTTPS tcp port 443 only and the client has all the authentication
pieces it needs in place via its pre-existing client certificate.  Additionaly, no extra configuration is required
in the client's client.rb.

That being said, there are no less than 12 scenarios supported by the audit cookbook as of v3.1.0:
 - Fetch Directly from Compliance : Report Directly to Compliance
 - Fetch Directly from Compliance : Report Directly to Automate
 - Fetch Directly from Compliance : Report to Compliance via Chef Server
 - Fetch Directly from Compliance : Report to Automate via Chef Server
 - Fetch from Compliance via Chef Server : Report Directly to Compliance
 - Fetch from Compliance via Chef Server : Report Directly to Automate
 - Fetch from Compliance via Chef Server : Report to Compliance via Chef Server
 - Fetch from Compliance via Chef Server : Report to Automate via Chef Server
 - Fetch From Automate via Chef Server : Report Directly to Compliance
 - Fetch From Automate via Chef Server : Report Directly to Automate
 - Fetch From Automate via Chef Server : Report to Compliance via Chef Server
 - Fetch From Automate via Chef Server : Report to Automate via Chef Server

To support all of the above scenarios, configuration can be required in up to 3 distinct locations:
 - client
   - client.rb
 - Chef Server
   - Chef Server + Compliance Server [Integration](https://docs.chef.io/integrate_compliance_chef_server.html)
   - chef-server.rb
 - Automate Server
   - delivery.rb

To understand exactly which settings to configure for any particular scenario I have created
this [cheat sheet](http://htmlpreview.github.io/?https://github.com/jeremymv2/audit-docs/blob/master/grid.html)
