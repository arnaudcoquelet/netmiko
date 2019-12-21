SROS-CLI
=======

Nokia SROS ssh library based on [Netmiko](https://ktbyers.github.io/netmiko) from [Kirk Byers](https://pynet.twb-tech.com)


## Installation

To install netmiko, simply us pip:

```
$ pip install netmiko
```

Netmiko has the following requirements (which pip will install for you)
- Paramiko >= 2.4.3
- scp >= 0.13.2
- pyserial
- textfsm


## Tutorials/Examples/Getting Started

### Tutorials:

- [Getting Started](https://pynet.twb-tech.com/blog/automation/netmiko.html)
- [Secure Copy](https://pynet.twb-tech.com/blog/automation/netmiko-scp.html)
- [Netmiko through SSH Proxy](https://pynet.twb-tech.com/blog/automation/netmiko-proxy.html)
- [Netmiko and TextFSM](https://pynet.twb-tech.com/blog/automation/netmiko-textfsm.html)
- [Netmiko and what constitutes done](https://pynet.twb-tech.com/blog/automation/netmiko-what-is-done.html)


### Example Scripts:

See the following directory for [example scripts](https://github.com/ktbyers/netmiko/tree/develop/examples/use_cases), including examples of:

- [Simple Connection](https://github.com/ktbyers/netmiko/blob/develop/examples/use_cases/case1_simple_conn/simple_conn.py)
- [Sending Show Commands](https://github.com/ktbyers/netmiko/tree/develop/examples/use_cases/case4_show_commands)
- [Sending Configuration Commands](https://github.com/ktbyers/netmiko/tree/develop/examples/use_cases/case6_config_change)
- [Handling Additional Prompting](https://github.com/ktbyers/netmiko/blob/develop/examples/use_cases/case5_prompting/send_command_prompting.py)
- [Connecting with SSH Keys](https://github.com/ktbyers/netmiko/blob/develop/examples/use_cases/case9_ssh_keys/conn_ssh_keys.py)
- [Cisco Genie Integration](https://github.com/ktbyers/netmiko/blob/develop/examples/use_cases/case18_structured_data_genie)


### Getting Started:

#### Create a dictionary representing the device.

Supported device_types can be found in [ssh_dispatcher.py](https://github.com/ktbyers/netmiko/blob/master/netmiko/ssh_dispatcher.py), see CLASS_MAPPER keys.
```py
from netmiko import ConnectHandler

cisco_881 = {
    'device_type': 'cisco_ios',
    'host':   '10.10.10.10',
    'username': 'test',
    'password': 'password',
    'port' : 8022,          # optional, defaults to 22
    'secret': 'secret',     # optional, defaults to ''
}

```

#### Establish an SSH connection to the device by passing in the device dictionary.

```py
net_connect = ConnectHandler(**cisco_881)
```

#### Execute show commands.

```py
output = net_connect.send_command('show ip int brief')
print(output)
```
```
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0              unassigned      YES unset  down                  down
FastEthernet1              unassigned      YES unset  down                  down
FastEthernet2              unassigned      YES unset  down                  down
FastEthernet3              unassigned      YES unset  down                  down
FastEthernet4              10.10.10.10     YES manual up                    up
Vlan1                      unassigned      YES unset  down                  down
```

## TextFSM Integration

Netmiko has been configured to automatically look in `~/ntc-template/templates/index` for the ntc-templates index file. Alternatively, you can explicitly tell Netmiko where to look for the TextFSM template directory by setting the `NET_TEXTFSM` environment variable (note, there must be an index file in this directory):

```
export NET_TEXTFSM=/path/to/ntc-templates/templates/
```

[More info on TextFSM and Netmiko](https://pynet.twb-tech.com/blog/automation/netmiko-textfsm.html).

