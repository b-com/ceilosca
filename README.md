ceilosca
========

Python plugin and storage driver for Ceilometer to send samples to monasca-api

### Installation Instructions for setting up Ceilosca manually

- Clone this project

- Install the module ceilosca
```shell
      # cd ceilosca
      # pip install --upgrade .
```

- Check that ceilosca entry points are correctly referenced:

```shell
      # pip install entry-point-inspector
      # epi group show ceilometer.metering.storage
      +------------+------------------------------------+------------+---------------------+---------------------------+
      | Name       | Module                             | Member     | Distribution        | Error                     |
      +------------+------------------------------------+------------+---------------------+---------------------------+
      | monasca    | ceilosca.storage.impl_monasca      | Connection | ceilosca 0.0.1.dev2 |                           |
      | sqlite     | ceilometer.storage.impl_sqlalchemy | Connection | ceilometer 6.0.0    |                           |
      | postgresql | ceilometer.storage.impl_sqlalchemy | Connection | ceilometer 6.0.0    |                           |
      | log        | ceilometer.storage.impl_log        | Connection | ceilometer 6.0.0    |                           |
      | mongodb    | ceilometer.storage.impl_mongodb    | Connection | ceilometer 6.0.0    |                           |
      | mysql      | ceilometer.storage.impl_sqlalchemy | Connection | ceilometer 6.0.0    |                           |
      | hbase      | ceilometer.storage.impl_hbase      | Connection | ceilometer 6.0.0    | No module named happybase |
      | db2        | ceilometer.storage.impl_db2        | Connection | ceilometer 6.0.0    |                           |
      +------------+------------------------------------+------------+---------------------+---------------------------+
      #
      # epi group show ceilometer.publisher
      +----------+-----------------------------------+-------------------------+---------------------+-----------------------+
      | Name     | Module                            | Member                  | Distribution        | Error                 |
      +----------+-----------------------------------+-------------------------+---------------------+-----------------------+
      | monasca  | ceilosca.publisher.monclient      | MonascaPublisher        | ceilosca 0.0.1.dev2 |                       |
      | udp      | ceilometer.publisher.udp          | UDPPublisher            | ceilometer 6.0.0    |                       |
      | direct   | ceilometer.publisher.direct       | DirectPublisher         | ceilometer 6.0.0    |                       |
      | file     | ceilometer.publisher.file         | FilePublisher           | ceilometer 6.0.0    |                       |
      | test     | ceilometer.publisher.test         | TestPublisher           | ceilometer 6.0.0    |                       |
      | notifier | ceilometer.publisher.messaging    | SampleNotifierPublisher | ceilometer 6.0.0    |                       |
      +----------+-----------------------------------+-------------------------+---------------------+-----------------------+
```

# License

```python
Copyright (c) 2016 B<>COM 2016

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
implied.
See the License for the specific language governing permissions and
limitations under the License.
```
