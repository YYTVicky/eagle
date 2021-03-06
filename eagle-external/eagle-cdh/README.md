<!--
{% comment %}
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to you under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->

EAGLE Parcel and CSD for Cloudera's CDH 5
=============
This Eagle Parcel and CSD greatly simplifies setting up a Eagle cluster on your Cloudera cluster.

## Table of Contents

- [Eagle Parcel and CSD for Cloudera's CDH 5](#eagle-parcel-and-csd-for-clouderas-cdh-5)
    - [Preparation](#preparation)
      - [1. Create Eagle Parcel](#1-create-eagle-parcel)
    - [Installation](#installation)
      - [1. Install the CSD](#1-install-the-csd)
      - [2. Downloading and Distributing Eagle Parcel](#2-downloading-and-distributing-eagle-parcel)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### Preparation

#### 1. Create Eagle Parcel

1. Download the eagle realse and decompression it.
2. Modify "eagle.conf" to "eagle.properties" in eagle-server.sh.Modify log path to specified path in server.yml.
3. Build the eagle parcel, please refer to [Building-a-parcel](https://github.com/cloudera/cm_ext/wiki/Building-a-parcel).

### Installation

#### 1. Install the CSD

1. In /apache-eagle/eagle-external/eagle-cdh,you can build it using the maven command "mvn assembly:assembly" and use the jar compiled in target folder
2. Upload the CSD jar to your Cloudera Manager node, place it in /opt/cloudera/csd/
3. Restart cloudera-scm-manager on Clouder Manager node:

```bash
service cloudera-scm-server restart
```
#### 2. Downloading and Distributing Eagle Parcel

1. Download your parcel file,generate .sha, and mainfest.json.
2. Copy your parcel files(.parcel, .sha, mainfest.json) to host /var/www/html/eagle
3. Go to your Cloudera Manager: http://cloudera_host:7180 and login with your admin credentials
4. Click on the parcels icon on the top right corner (next to the search bar)
5. Click on "Edit Settings"
6. Add a new value in "Remote Parcel Repository URLs", enter the IP address for the machine on which you just setup your HTTP server, for example: http://hostname/eagle
7. Save your changes and go back to Parcels page by clicking on the Parcels icon on the top right corner (next to the search bar)
8. Click on "Check for New Parcels"
9. You should see "Eagle" parcel in the list. Download it, then distribute it and activate it
10. You will be prompted to restart your cluster, click "Restart". Once that's done, you will need to restart "Cloudera Management Service" manually as well
11. Now you should be able to simply add your new Eagle service through CM. (click on the little arrow next your cluster name and click "Add Service", follow the wizard instructions)