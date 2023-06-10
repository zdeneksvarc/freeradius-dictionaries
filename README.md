# freeradius-dictionaries

## About

FreeRADIUS dictionaries extracted from FreeRADIUS release 3.2.3 (May 26, 2023).
- https://github.com/FreeRADIUS/freeradius-server/releases

## Notes about DHCP Option82 injected by RouterOS bridge

- Configuration (RouterOS v7.9.2)
```
/ip dhcp-server set <bridge> address-pool=static-only
/ip dhcp-server config set radius-password=same-as-user|empty
/interface bridge set <bridge> dhcp-snooping=yes add-dhcp-option82=yes
```

- RouterOS sends DHCP Option82 values (Agent-Remote-Id, Agent-Circuit-Id, ADSL-Agent-Remote-Id, ADSL-Agent-Circuit-Id) as string not as octets. However, these AVPs are defined as octets in dictionaries (dictionary.rfc4679, dictionary.ericsson.ab).
- You can rewrite data type for these AVP in these dictionaries (octets > string) if you use only RouterOS NAS devices.
- Or you can use dictionaries as they are and convert the hexadecimal values to the string if you get a message with Option82 from RouterOS.
- Quick test: `echo "hexadecimal" | xxd -r -p`