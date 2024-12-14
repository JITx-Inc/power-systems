# Installation

In slm.toml add:
```
power-systems = { git = "JITx-Inc/power-systems", version = "0.5.0" }
```

# filters
## unbalanced-filter
Construct an unbalanced filter with `power` inputs/outputs

This module creates an unbalanced filter, typically used with a ferrite, resistor, or other 2-pin device.

An unbalanced filter places one device in series with the `V+` rail. The `V-` is directly coupled from input to output.
```
inst filt-VPLL : unbalanced-filter(passives/ferrite/BLM18KG(220))
```
### ports
```
  port vin : power
  port vout : power
```
### Parameters
- comp:Instantiable - Component that will be instantiated to create the filter. This component is expected to be a two-pin device. If this device is polarized then the anode `a` is connected to vin and the cathode `c` is connected to vout
by default.
--
- flip:True|False = false  If this parameter is true, the instantiated component is flipped - `c` connects to `vin` and `a` connects to `vout`.

## diode-OR
Construct a diode-OR of multiple inputs
```
  inst OR : power-systems/filters/diode-OR(diodes/SSA33L/component, 3)
```
### ports
```
  port vin : power[num-inputs]
  port vout : power
```
### Parameters
- comp:Instantiable - Component that will be instantiated to create the filter. Same attachment behavior as unbalanced-filter
- num-inputs:Int - how many inputs into the diode-OR circuit
