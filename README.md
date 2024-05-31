# Project LATiTuDeS
***Library of Aquatic Tracking and Telemetry Data Samples***

## Library structure

```
latitudes/
  |-- Raw/
     |-- Vendor1/
          |-- InstrumentA/
               |-- software version 1.0/
                    |-- file123.ext
                    |-- metadata.yaml
          |-- ...
     |-- Vendor2/
     |-- ...
  |-- Derived/
     |-- Network1/
     |-- Network2/
     |-- ...
  |-- Network Schema/
  |-- Forms/
```

## File metadata schema
Files must be associated with a `metadata.yaml` file providing its context, attribution, and licensing. The current schema is found within [`schema-guide.md`](schema-guide.md) and validated against those schema in the `schema/` directory.

## Contributing and data needs
- Raw
   - Vemco/Innovasea (Current: VRL, VDAT; Legacy: binary, text)
   - Lotek
   - ThelmaBiotel
   - Sonotronics
- Derived
   - Vemco/Innovasea ("non-truth" VRL, CSV)
   - OTN matched/unmatched/qualified/unqualified/other networks
   - GLATOS and `glatos`
   - ETN and `etn`
   - IMOS
   - Actel
   - Deployment data, various forms
- Forms
   - OTN/FACT/MATOS/ETN/GLATOS metadata forms (multiple versions)
- Schema
   - OTN (multiple across Geoserver and exports)
   - GLATOS 

## Licensing

Project LATiTuDeS is licensed under the [CC-BY-4.0 license](licenses/LICENSE-CC-BY-4.0.md).

Files are individually-licensed under the license reported in the `license` field of its corresponding `metadata.yaml` file.

All licenses can be found in the [`licenses/` directory](licenses).