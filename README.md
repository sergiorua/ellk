ELK Cookbook
============

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

manage elasticsearch, logstash, logstash-forwarder and kibana

*note: expects consumer to install java and handle certs*

Support and Tested
------------
centos66

Requirements
------------
- chef 11+
- some kind of java
- see [metadata](/metadata.rb) for complexity

About
------------
See [elktest](/test/cookbooks/elktest/recipes/default.rb) about how to use.


LOGSTASH-FORWARDER
------------
Installs a go binary with source, checksum as user, group to /opt/logstash-forwarder.  
The config file then is generated with certificate, key locations, an array of `logstash`
servers and finally a array of hashes is converted to JSON for the `files` structure.

```
logstash_forwarder 'default' do
  crt_location '/tmp/logstash.crt'
  key_location '/tmp/logstash.key'
  logstash_servers ['localhost:5043']
  files [{ 'paths' => ['/var/log/messages', '/var/log/*log'], 'fields' => { 'type' => 'syslog' } }]
end
```

Contributing
------------
1. Fork the repository on Github
2. Create a named feature branch (like `add_component_x`)
3. Write your change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using Github

License and Authors
-------------------
Author: Jacob Dearing // jacob.dearing@gmail.com

```
The MIT License (MIT)

Copyright (c) 2015 Jacob Dearing

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
