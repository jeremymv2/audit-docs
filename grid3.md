<table>
<tr>
  <th>Fetch Directly From Compliance</th>
  <td><b>Report Directly to Compliance</b>
<pre lang="ruby">
['audit']['reporter'] = 'chef-compliance'
['audit']['server'] = 'https://compliance-server.test/api'
['audit']['refresh_token' OR 'token'] = '..'
['audit']['owner'] = 'User/Org'
</pre>
<p><b>Report Directly to Automate</b>
<pre lang="ruby"><code>
['audit']['reporter'] = 'chef-automate'
['audit']['server'] = 'https://compliance-server.test/api'
['audit']['refresh_token' OR 'token'] = '..'
['audit']['owner'] = 'User/Org'

## client.rb:
data_collector['server_url'] = 'https://automate-server.test/data-collector/v0/'
data_collector['token'] = '..'
</code></pre>
<p><b>Report to Compliance via Chef Server</b>
<pre lang="ruby">
['audit']['reporter'] = 'chef-server-compliance'
['audit']['server'] = 'https://compliance-server.test/api'
['audit']['refresh_token' OR 'token'] = '..'
['audit']['owner'] = 'User/Org'
</pre>
<p><b>Report to Automate via Chef Server</b>
<pre lang="ruby">
['audit']['reporter'] = 'chef-server-automate'
['audit']['server'] = 'https://compliance-server.test/api'
['audit']['refresh_token' OR 'token'] = '..'
['audit']['owner'] = 'User/Org'

# chef-server.rb:
data_collector['root_url'] = 'https://automate-server.test/data-collector/v0/'
</pre>
  </td>
</tr>
<tr>
  <th>Fetch From Compliance via Chef Server</th>
  <td><b>Report Directly to Compliance</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-compliance'
    ['audit']['fetcher'] = 'chef-server'
    ['audit']['server'] = 'https://compliance-server.test/api'
    ['audit']['refresh_token' OR 'token'] = '..'
    ['audit']['owner'] = 'User/Org'

    Compliance Integrated w/ Chef Server
    </pre>
    <p><b>Report Directly to Automate</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-automate'
    ['audit']['fetcher'] = 'chef-server'
    ['audit']['server'] = 'https://compliance-server.test/api'
    ['audit']['refresh_token' OR 'token'] = '..'
    ['audit']['owner'] = 'User/Org'

    Compliance Integrated w/ Chef Server

    client.rb:
      data_collector['server_url'] = 'https://automate-server.test/data-collector/v0/'
      data_collector['token'] = '..'
    </pre>
    <p><b>Report to Compliance via Chef Server</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-server-compliance'
    ['audit']['fetcher'] = 'chef-server'

    Compliance Integrated w/ Chef Server
    </pre>
    <p><b>Report to Automate via Chef Server</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-server-automate'
    ['audit']['fetcher'] = 'chef-server'

    Compliance Integrated w/ Chef Server

    chef-server.rb:
      data_collector['root_url'] = 'https://automate-server.test/data-collector/v0/'</td>
    </pre>
  </td>
</tr>
<tr>
  <th>Fetch From Automate via Chef Server</th>
  <td><b>Report Directly to Compliance</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-compliance'
    ['audit']['fetcher'] = 'chef-server'
    ['audit']['server'] = 'https://compliance-server.test/api'
    ['audit']['refresh_token' OR 'token'] = '..'
    ['audit']['owner'] = 'User/Org'

    chef-server.rb:
      profiles['root_url'] = 'https://automate-server.test'

    delivery.rb:
      compliance_profiles["enable"] = true
    </pre>
    <p><b>Report Directly to Automate</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-automate'
    ['audit']['fetcher'] = 'chef-server'

    chef-server.rb:
      profiles['root_url'] = 'https://automate-server.test'

    client.rb:
      data_collector['server_url'] = 'https://automate-server.test/data-collector/v0/'
      data_collector['token'] = '..'

    delivery.rb:
      compliance_profiles["enable"] = true
    </pre>
    <p><b>Report to Compliance via Chef Server</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-server-compliance'
    ['audit']['fetcher'] = 'chef-server'

    Compliance Integrated w/ Chef Server

    chef-server.rb:
      profiles['root_url'] = 'https://automate-server.test'

    delivery.rb:
      compliance_profiles["enable"] = true
    </pre>
    <p><b>Report to Automate via Chef Server</b>
    <pre lang="ruby">
    ['audit']['reporter'] = 'chef-server-automate'
    ['audit']['fetcher'] = 'chef-server'

    chef-server.rb:
      data_collector['root_url'] = 'https://automate-server.test/data-collector/v0/'
      profiles['root_url'] = 'https://automate-server.test'

    delivery.rb:
      compliance_profiles["enable"] = true
    </pre>
  </td>
</tr>
</table>
