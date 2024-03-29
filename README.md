# Project LATiTuDeS
***Library of Aquatic Tracking and Telemetry Data Samples***

## Library structure

## File metadata schema
Data files must be associated with a `metadata.yaml` file providing context and attribution for the data file. The current schema is found within [`schema-guide.md`](schema-guide.md) and validated against [`test/validation-schema.yaml`](test/validation-schema.yaml).

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
