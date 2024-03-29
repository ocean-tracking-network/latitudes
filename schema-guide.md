# Guide to metadata schema version 0.0.0.9000

This guide is adapted directly from the [CITATION.cff schema guide](https://github.com/citation-file-format/citation-file-format/blob/main/schema-guide.md).

Valid metadata schema:

  - Are valid YAML 1.2 ([specification](http://yaml.org/spec/1.2/spec.html), [validator](http://www.yamllint.com/));
  - Contain valid CITATION.cff YAML as outlined in the [CITATION.cff schema guide](https://github.com/citation-file-format/citation-file-format/blob/main/schema-guide.md)
  
Beyond that, everything is fluid at this point. If you would like to include new fields, please do (and document them appropriately!). If you believe that one of the current fields is not useful for your data, please file an issue to let us know why and we'll flip the switch.


## Index

### Keys

  - [`citation.cff`](#citation.cff)
  - [`creation_date`](#creation_date)
  - [`exporting_software`](#exporting_software)
  - [`name`](#name)
  - [`file_type`](#file_type)
  - [`format`](#format)
  - [`instrument`](#instrument)
  - [`license`](#license)
  - [`poc`](#poc)
  - [`recording`](#recording)
  - [`records`](#records)
  - [`size_bytes`](#size_bytes)
  
### Definitions

  - [`definitions.code_map`](#definitions.code_map)
  - [`definitions.date`](#definitions.date)
  - [`definitions.datetime`](#definitions.datetime)
  - [`definitions.environment`](#definitions.environment) (object)
  - [`definitions.exporting_software`](#definitions.exporting_software) (object)
  - [`definitions.instrument`](#definitions.instrument) (object)
  - [`definitions.poc`](#definitions.poc) (object)
  - [`definitions.recording`](#definitions.recording) (object)
  - [`definitions.records`](#defintions.records) (object)
  - [`definitions.transmitter`](#definitions.transmtiter) (object)
  - [`definitions.type`](#definitions.type)
  - [`defintions.vendor`](#definitions.vendor)
  - [`defintions.version`](#definitions.version)




## Keys

### `citation.cff`

  - **type**: CITATION.cff YAML
  - **required**: `true`
  - **description**: Valid Citation File Format YAML as outlined in the [CITATION.cff schema guide](https://github.com/citation-file-format/citation-file-format/blob/main/schema-guide.md)
  - **usage**:<br><br>
      ``` yaml
      cff-version: 1.2.0
      title: "filename_xyz.vrl"
      authors:
        - family-names: Pye
          given-names: Jonathan
      message: "If you use this software, please cite it using these metadata."
      ```

### `creation_date`

  - **type**: [`definitions.date`](#definitions.date)
  - **required**: `true`
  - **description**: Date on which file was created in YYYY-MM-DD format.
  - **usage**:<br><br>
      ``` yaml
      creation_date: 2024-01-01
      ```

### `exporting_software`

  - **type**: Array of [`definitions.exporting_software`](#definitions.exporting_software)
  - **required**: `true`
  - **description**: Software that created the file
  - **usage**:<br><br>
      ``` yaml
      exporting_software:
        name: VR2PC
        version: 1.00
      ```
    
### `name`

  - **type**: string
  - **required**: `true`
  - **description**: Name of the data file 
  - **usage**:<br><br>
      ``` yaml
      name: my_file.vrl
      ```
    
### `file_type`

  - **type**: string
  - **required**: `true`
  - **description**: raw detections, derived detections, network schema
  - **usage**:<br><br>
      ``` yaml
      file_type: raw detections
      ```
    
### `format`

  - **type**: string
  - **required**: `true`
  - **description**: File format. ASCII text, VRL, VDAT, XLSX, etc.
  - **usage**:<br><br>
      ``` yaml
      format: VDAT
      ```
    
### `instrument`

  - **type**: Array of [`definitions.instrument`](#definitions.instrument)
  - **required**: `false`
  - **description**: Required for raw and derived detection file types.
  - **usage**:<br><br>
      ``` yaml
      instrument:
        type: "VR2W-069.0k"
        frequency_khz: 69
        vendor: Vemco
        firmware_version: 1.03
        code_map: MAP-112
      ```

### `license`

  - **type**: string
  - **required**: `true`
  - **description**: License under which your data can be used, distributed, etc.
  For help selecting a license, try the [Creative Commons License Chooser](https://chooser-beta.creativecommons.org/).
  - **usage**:<br><br>
      ``` yaml
      license: CC-BY-NC-SA-4.0
      ```


### `poc`

  - **type**: Array of [`definitions.poc`](#definitions.poc)
  - **required**: `true`
  - **description**: Point of contact for the described data. Must include a name and email contact.
  - **usage**:<br><br>
      ``` yaml
      poc:
        name: Jane Point-of-contact
        email: theemail@email.com
      ```

### `recording`

  - **type**: Array of [`definitions.recording`](#definitions.recording) containing
  items of [`definitions.datetime`](#definitions.datetime)
  - **required**: `false`
  - **description**: Start and end date-times of receiver recording period.
  - **usage**:<br><br>
      ``` yaml
      recording:
        start: "2023-01-01T00:00:00Z"
        end: "2024-01-01T00:00:00Z"
      ```
    
### `records`

  - **type**: Array of [`definitions.records`](#defintions.records)
  - **required**: `true`
  - **description**: Summary of logged data.
  - **usage**:<br><br>
      ``` yaml
      records:
        transmitter:
        - type: "4K Pinger"
          vendor: Vemco
          n_detected: 6
          n_detections: 827
        environment:
        - type: temperature
          min: -4
          max: 30
      ```
    
### `size_bytes`

  - **type**: int
  - **required**: `true`
  - **description**: File size in bytes
  - **usage**:<br><br>
      ``` yaml
      size_bytes: 12345
      ```

## Definitions

***!!! THIS SECTION HAS BEEN COPIED FROM CITATION.CFF AND IS CURRENTLY UNDERGOING ADAPTATION.***

Some values in CFF files are valid in different keys. For example, `repository-code`, `url` and `license-url` all take URLs as values.

The schema therefore has [*definitions*](https://json-schema.org/understanding-json-schema/structuring.html#definitions) of smaller subschemas, that can be reused in the schema from the respective key, instead of having to duplicate them. For example, there is one definition for a valid URL value ([`definitions.url`](#definitionsurl)), that is being referenced from `repository-code`, `url` and `license-url`.

**Note:** `definitions` and its subkeys like `definitions.poc` or `definitions.recording` should not be used as keys in metadata files:
```yaml
# incorrect
poc:
  - definitions.poc.name: "Mike O'Brien"
```
```yaml
# incorrect
poc:
  - definitions:
      name: "Mike O'Brien"
```
```yaml
# correct
poc:
  - name: "Mike O'Brien""
```




### definitions.code_map

  - **type**: string or [`definitions.code_map.custom`](#definitions.code_map.custom)
  - **required**: `true` for `definitions.instrument`
  - **description**:
  - **usage**:<br><br>
      ``` yaml
      code_map: MAP-114
      ```
      ``` yaml
      code_map: Generation 2
      ```
      ``` yaml
      code_map:
        custom:
          - type: "4K Pinger"
            sync: 380.0
            bin: 20.0
      ```

#### definitions.code_map.custom

  - **type**: `object` with the following keys:
    - [`bin`](#definitions.code_map.custom.bin)
    - [`sync`](#definitions.code_map.custom.sync)
    - [`type`](#definitions.type)
  - **required**: `false`
  - **description**:
  - **usage**:<br><br>
      ``` yaml
      custom:
        - type: "4K Pinger"
          sync: 380.0
          bin: 20.0
      ```

##### definitions.code_map.custom.bin

  - **type**: float
  - **required**: `true` for `defintions.code_map.custom`
  - **description**: Programmed bin size of the target transmitter type in mSec
  - **usage**: see [`definitions.code_map.custom`](#definitions.code_map.custom)

##### definitions.code_map.custom.sync

  - **type**: float
  - **required**: `true` for `defintions.code_map.custom`
  - **description**: Programmed sync value of the target transmitter type in mSec
  - **usage**: see [`definitions.code_map.custom`](#definitions.code_map.custom)




### definitions.date

  - **type**: Nonempty string
  - **required**: `NA`
  - **description**: UTC date in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601).
  That is, 4 digit year, 2 digit month, and 2 digit day separated by hyphens.
  (YYYY-mm-dd)
  - **usage**:<br><br>
      ``` yaml
      start: "2024-01-01"
      ```
      ``` yaml
      creation_date: "2024-12-31"
      ```




### definitions.datetime

  - **type**: Nonempty string
  - **required**: `NA`
  - **description**: UTC date-times in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601).
  That is, 4 digit year, 2 digit month, and 2 digit day separated by hyphens;
  a capital "T"; 2 digit hour, 2 digit minute, and 2 digit second separated by colons;
  and a capital "Z". (YYYY-mm-ddTHH:MM:SSZ)
  - **usage**:<br><br>
      ``` yaml
      start: "2024-01-01T00:00:00Z"
      ```
      ``` yaml
      end: "2024-12-31T11:59:59Z"
      ```




#### definitions.environment

  - **type**:  `object` with the following keys:
    - [`TBD`]()
  - **required**: `NA`
  - **description**: 
  - **usage**:<br><br>
      ``` yaml
      ```




### definitions.exporting_software

  - **type**: `object` with the following keys:
    - [`name`](#definitions.exporting_software.name)
    - [`version`](#definitions.version)
  - **required**: `NA`
  - **description**: Data on the software instance which produced the file
  - **usage**:<br><br>
      ``` yaml
      exporting_software:
        name: VUE
        version: 1.00
      ```

#### definitions.exporting_software.name

  - **type**: str
  - **required**: `true` for `exporting_software` record
  - **description**: Name of the software which produced the file
  - **usage**: see [`definitions.exporting_software`](#definitions.exporting_software)
  



### definitions.instrument

  - **type**: `object` with the following keys:
    - [`code_map`](#definitions.code_map)    
    - [`firmware_version`](#definitions.instrument.firmware_version)
    - [`frequency_khz`](#definitions.instrument.frequency_khz)
    - [`serial_number`](#definitions.instrument.serial_number)
    - [`type`](#definitions.type)
    - [`vendor`](#definitions.vendor)
  - **required**: `NA`
  - **description**: An instrument.
  - **usage**:<br><br>
      ``` yaml
      instrument:
        type: "VR2C-069.0k"
        frequency_khz: 69
        vendor: Vemco
        firmware_version: 9.99
        code_map: Generation 2
        serial_number: 3145
      ```


#### definitions.instrument.firmware_version

  - **type**: `definitions.version`
  - **required**: `true` for `instrument` record
  - **description**:
  - **usage**: see [`definitions.instrument`](#definitions.instrument) and
  [`definitions.version`](#definitions.version)

#### definitions.instrument.frequency_khz

  - **type**: int
  - **required**: `true` for `instrument` record
  - **description**: Frequency at which the instrument is listening in kilohertz
  - **usage**:<br><br>
      ``` yaml
      instrument:
        frequency_khz: 69
      ```
      ``` yaml
      instrument:
        frequency_khz: 180
      ```

#### definitions.instrument.serial_number

  - **type**: string
  - **required**: `true` for `instrument` record
  - **description**: Instrument serial number
  - **usage**: see [`definitions.instrument`](#definitions.instrument)




### definitions.poc

  - **type**: `object` with the following keys:
    - [`name`](#definitions.poc.name)
    - [`email`](#definitison.poc.email)
  - **required**: `true`
  - **description**: Information on the point of contact for the data file
  - **usage**:<br><br>
      ``` yaml
      poc:
        name: Jon Pye
        email: jonsemail@email.edu
      ```

#### definitions.poc.name

  - **type**: string
  - **required**: `true`
  - **description**: Name of the point of contact
  - **usage**: see [`definitions.poc`](#definitions.poc)

#### definitions.poc.email

  - **type**: `object` with the following keys:
    - `name`
    - `email`
  - **required**: `true`
  - **description**: Email address of the point of contact
  - **usage**: see [`definitions.poc`](#definitions.poc)



     
### definitions.recording

  - **type**: `object` with the following keys:
    - [`start`](#definitions.recording.start)
    - [`end`](#definitions.recording.end)
  - **required**: `NA`
  - **description**: File size in bytes
  - **usage**:<br><br>
      ``` yaml
      recording:
        start: '2024-01-01T00:00:00Z'
        end:  '2024-12-31T11:59:59Z'
      ```
      
#### definitions.recording.start

  - **type**: [`definitions.datetime`](#defintions.datetime)
  - **required**: `true`
  - **description**: Date-time of start of instrument recording
  - **usage**: see [`definitions.recording`](#definitions.recording) and
  [`definitions.datetime`](#definitions.datetime)

#### definitions.recording.end

  - **type**: [`definitions.datetime`](#defintions.datetime)
  - **required**: `true`
  - **description**: Date-time of end of instrument recording
  - **usage**: see [`definitions.recording`](#definitions.recording) and
  [`definitions.datetime`](#definitions.datetime)




### defintions.records

  - **type**: `object` with the following keys:
    - [`transmitter`](#definitions.transmitter)
    - [`environment`](#definitions.environment)
  - **required**: `NA`
  - **description**: Summary of logged data.
  - **usage**: see [`records`](#records)




### definitions.transmitter

  - **type**: `object` with the following keys:
    - [`type`](#definitions.type)
    - [`vendor`](#definitions.vendor)
    - [`n_detected`](#definitions.transmitter.n_detected)
    - [`n_detections`](#definitions.transmitter.n_detections)
  - **required**: `NA`
  - **description**:
  - **usage**:<br><br>
      ``` yaml
      transmitter:
      - type: "4K Pinger"
        vendor: Vemco
        n_detected: 6
        n_detections: 827
      ```

#### definitions.transmitter.n_detected

  - **type**: int
  - **required**: `true` for `definitions.transmitter`
  - **description**: Total number of reported individuals detected
  - **usage**: see [`definitions.transmitter`](#definitions.transmitter)

#### definitions.transmitter.n_detections

  - **type**: int
  - **required**: `true` for `definitions.transmitter`
  - **description**: Total number of reported detections
  - **usage**: see [`definitions.transmitter`](#definitions.transmitter)
      
      
      

### definitions.type

  - **type**: string
  - **required**:
    - `true` for [`definitions.instrument`](#definitions.instrument) and [`definitions.code_map.custom`](#definitions.code_map_custom)
  - **description**: Type or style of the recording instrument or transmitter.
  The more specific, the better.
  - **usage**:<br><br>
      ``` yaml
      instrument:
        type: "VR2C-069.0k"
      ```
      ``` yaml
      instrument:
        type: "VR2-069.0k-1.03-2-1431-C"
      ```
      ``` yaml
      transmitter:
        type: "V16-TP"
      ```




### definitions.vendor

  - **type**: string
  - **required**:
    - `true` for [`definitions.instrument`](#definitions.instrument)
    - `false` for [`definitions.records.transmitter`](definitions.records.transmitter)
  - **description**: Instrument or transmitter vendor
  - **usage**:<br><br>
      ``` yaml
      instrument:
        vendor: Innovasea
      ```
      ``` yaml
      transmitter:
        - vendor: Lotek
      ```




### definitions.version

  - **type**: string
  - **required**: `NA`
  - **description**: Version of the software or firmware which produced the file
  - **usage**:<br><br>
      ``` yaml
      instrument:
        firmware_version: 5.2
      ```
      ``` yaml
      exporting_software:
        version: 1.1.0
      ```