<!--
#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#  KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
-->

# Apache Mynewt for UBlox NINA-B3

## Overview

This is a mynewt project skeleton for quickly and easily building the blehci
firmware that can be flashed to the SolidRun SolidSense platforms with UBlox NINA-B3.
This firmware allows the NINA-B3 to act like a normal HCI device and is compatible
with newer Bluez stacks.

## Building

Apache mynewt for UBlox NINA-B3 contains targets to allowing building the boot and blehci image
that when executed on the NINA-B3 allows it to act under Linux as a normal HCI device using the
traditional Bluez stack.

1. Download and install Apache Newt.

You will need to download the Apache Newt tool, as documented in the [Getting Started Guide](https://mynewt.apache.org/latest/get_started/index.html).

2. Download the Apache Mynewt Core package and subsequent additional packages required for the boot and blehci
images (executed from the mynewt-sr-nina-b3 directory).

```no-highlight
    $ newt upgrade
```

3. Build the Newt bootloader for the NINA-B3 using the "nina-b3_boot" target
(executed from the mynewt-sr-nina-b3 directory).

```no-highlight
    $ newt build nina-b3_boot
```

4. Build the blehci application for the NINA-B3 using the "nina-b3_blehci" target
(executed from the mynewt-sr-nina-b3 directory).

```no-highlight
    $ newt build nina-b3_blehci
    $ newt create-image nina-b3_blehci 1.8.1
```

### Initializing under Linux 

The device should now be ready to be initialized under Linux.

```no-highlight
sudo btattach -B /dev/ttymxc3 -S 1000000 -N
```

The hci interface should now be available.

```no-highlight
hciconfig
hci0:	Type: Primary  Bus: UART
	BD Address: BB:EC:E6:0D:DC:04  ACL MTU: 255:12  SCO MTU: 0:0
	UP RUNNING 
	RX bytes:231 acl:0 sco:0 events:16 errors:0
	TX bytes:112 acl:0 sco:0 commands:16 errors:0
```
