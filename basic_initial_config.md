Note: These commands work on both Cisco routers and switches.

## Basic device configuration 

Command|Additional Notes
---|---
``CDevice>enable``|
``CDevice#configure terminal``|
``CDevice(config)#no ip domain-lookup``|disable DNS lookup
``CDevice(config)#cdp run``|ensure CDP is running :bulb:(although it is running on Cisco devices by default)
``CDevice(config)#banner motd $ message $``| set banner
``CDevice(config)#hostname nameofhost``| set hostname to nameofhost
``CDevice(config-line)#logging synchronous``|
``CDevice(config-line)#history size [lines]``|specify the size (number of lines) for the history of executed commands (you can view your history with ``R1#show history``)
``CDevice(config-line)#exec-timeout [minutes] [seconds]``|
``CDevice(config-line)#end``|exit to EXEC privileged mode, where the next command will be executed
``CDevice#copy running-config startup-config``|Saves the running configuration to the NVRAM


## Security settings

| Command                           | Additional Notes                                              |
|-----------------------------------|-------------------------------------------------------------|
| `CDevice(config)#enable secret s8cr8t` | Set enable password (encrypted privileged EXEC password) to `s8cr8t` |
| `CDevice(config)#line console 0`<br>`CDevice(config-line)#password p@ssw0rd`<br>`CDevice(config-line)#login`<br>`CDevice(config-line)#exit`  | Set console password to `p@ssw0rd`                          |
| `CDevice(config)#security password min-length 8` | Set minimum password length to 8                             |
| `CDevice(config)#service password-encryption` | Encrypt all plaintext passwords
| `CDevice(config)#username user secret cisco` | Create user 'user' with password 'cisco'

## Configuring SSH
Command|Description
---|---
| `CDevice#show ip ssh`|Use it to verify that the switch supports SSH
| `CDevice(config)#ip domain-name [domain-name]`|
| `CDevice(config)#crypto key generate rsa general-keys modulus 4096`| Generate an RSA crypto key using 4096 bits modulus
| `CDevice(config)#username [admin] secret [ccna]`|
| `CDevice(config)#username user secret cisco` | Create user 'user' with password 'cisco'
| `CDevice(config)#line vty 0 15`<br>`CDevice(config-line)#login local`<br>`CDevice(config-line)#transport input ssh`<br>`CDevice(config-line)#exit`  | Configure the vty lines to accept SSH access only
| `CDevice(config)##ip ssh version 2`|enable SSH version 2
| `CDevice(config)##crypto key zeroise rsa`|:warning: use to **delete** RSA key pair

### Modifying SSH configuration
Command|Description
---|---
| `CDevice(config)##ip ssh time-out [time]`|Change timeout setting (time in seconds)
| `CDevice(config)##ip ssh authentication-retries [retries]`|Change number of allowed authentication attempts

Verify your newly configured settings with ``S1#show ip ssh``

----

You can copy the same sequence, contained in the text box below, and paste it in your Cisco device, whether it is a real-world physical Cisco device, or a simulated device in an environment like Packet Tracer.  
:bulb: Note that the commands below are abbreviated. Still. They should work just fine.  
:bulb: Be sure to select and copy up to the blank line below the last command. That way, such last command will be executed without you having to manually press enter. 

```
ena
conf t
no ip domain-lookup
cdp run
line con 0
logging syn
his size 50
exec-timeout 25 0
end
copy run start

<< select and copy up to the line above this "marker" with your cursor
```

## Other tips and hints for your initial configurations
:bulb:If there are non-Cisco devices on your network, you might also want to enable LLDP (Link-Layer Discovery Protocol), use:  
````CDevice(config)#lldp run````
