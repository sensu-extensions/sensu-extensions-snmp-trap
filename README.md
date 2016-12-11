# Sensu SNMP Trap Check Extension

Creates a SNMPv2 trap listener as part of the Sensu client process.
This SNMP trap extension loads MIBs and attempts to translate SNMP
traps into Sensu check results.

## Inspiration

This SNMP trap extension was inspired by the work done by Toby Jackson
on [SNMPTrapHandler](https://github.com/warmfusion/sensu-extension-snmptrap).

## Installation

On a Sensu client machine.

For Sensu version < 0.27:

```
/opt/sensu/embedded/bin/gem install sensu-extensions-snmp-trap -v 0.0.19
```

For Sensu version >= 0.27:

```
sensu-install -e snmp-trap:0.0.19
```

Edit `/etc/sensu/conf.d/extensions.json` to load it.

``` json
{
  "extensions": {
    "snmp-trap": {
      "version": "0.0.19"
    }
  }
}
```

## Configuration

Edit `/etc/sensu/conf.d/snmp_trap.json` to change its configuration.

``` json
{
  "snmp_trap": {
    "community": "secret"
  }
}
```

|attribute|type|default|description|
|----|----|----|---|
|bind|string|0.0.0.0|IP to bind the SNMP trap listener to|
|port|integer|1062|Port to bind the SNMP trap listener to|
|community|string|"public"|SNMP community string to use|
|mibs_dir|string|"/etc/sensu/mibs"|MIBs directory to import and load MIBs from|
|imported_dir|string|"$TMPDIR/sensu_snmp_imported_mibs"|Directory to store imported MIB data in|
|handlers|array|["default"]|Handlers to specify in Sensu check results|
