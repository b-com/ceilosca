ceilosca
========

Python plugin and storage driver for OpenStack Telemetry service, i.e. 
Ceilometer, to send samples to Monasca API.

This python project is a complete refactoring of the project 
[monasca-ceilometer](https://github.com/openstack/monasca-ceilometer).

### Installation Pre-requisites
You have to install the Telemetry service according to this
[documentation](http://docs.openstack.org/mitaka/install-guide-ubuntu/ceilometer-install.html). 

### Installation Instructions for setting up Ceilosca manually

- Clone this project

- Install the module ceilosca
```shell
      # cd ceilosca
      # pip install --upgrade .
```

- Check that ceilosca entry points (named ``monasca``) are correctly referenced, 
without errors:

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


# Configuration
You have to configure the Telemetry service in order to use Ceilosca as the 
storage backend and the publisher default driver as well.

## Set Ceilosca as the default storage backend
Edit the file ``/etc/ceilometer/ceilometer.conf`` and update the parameter
``metering_connection`` with the Manasca API URL.

```shell
# The connection string used to connect to the metering database. (if
# unset, connection is used) (string value)
#metering_connection = <None>
metering_connection = monasca://http://<MONASCA_API_IP>:8070/v2.0

```

You will find an example in etc/ceilometer directory.

## Set Ceilosca as the default publisher
Update the file ``/etc/ceilometer/pipeline.yaml`` in order to forward the
metrics to Monasca API, by addding ``publishers`` URL.

You will find an example in etc/ceilometer directory.

## Add the customized metrics fowarded to Monasca
Copy/Paste the file ``etc/ceilometer/monasca_field_definitions.yaml`` into 
``/etc/ceilometer`` directory. This file contains filtering keys used by the
``MonascaDataFilter`` class to forward to Monasca API a metric with a subset
of the original sample fields.

## Configure the credentials
Check in the file ``/etc/ceilometer/ceilometer.conf`` the section
 ``service_credentials``. Username defined in this section must have a correct 
 role to access to the Monasca API. For more information, read this 
 [documentation](http://docs.openstack.org/admin-guide/identity-concepts.html)

# Testing
You can run unitaty tests by using the ``tox`` command:
```shell
      # cd ceilosca
      # tox -epy27
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
