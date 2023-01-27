# Data Size Kata

A coding kata that focuses on domain-driven design, encapsulation, and reducing primitive obsession.

## Intro

Our application deals with file sizes, storage sizes, download sizes, etc. Depending on use case, locale, user settings, or other factors, these data sizes can be displayed to the user as well as provided/consumed by different APIs in different formats.

## Design Goal

- No static utils, no primitive obsession, no explicit conversions.
- Immutable.
- Usage examples (Java):<br>
  `DataSize fileSize = DataSize.fromBytes(Files.size(filePath));`<br>
  `long bytes = downloadSize.asBytes();`<br>
  `BigDecimal gigabytes = downloadSize.asGigabytes();`<br>
  `DataSize dataSize = DataSize.parse("1337.42 kB");`<br>
  `DataSize totalFileSize = fileSize1.plus(fileSize2);`<br>
  `String humanFriendlyFileSize = fileSize.formatHumanFriendly();`<br>
  `String formattedFileSizeInMB = fileSize.format("MB");`<br>

## Requirements

### 1. Formatting

A data size can be formatted as a human-friendly string according to the following rules:
  - Use the largest unit (out of B, kB, MB, GB, TB) without leading zeros.<br>
    (e.g. 123 bytes => "123 B", 30010 bytes => "30.01 kB")
  - No trailing zeros.<br>
    (e.g. 1000 bytes => "1 kB", not "1.0 kB")
  - Up to 2 digits after the decimal point, rounding if necessary.<br>
    (e.g. 10029421 bytes => "10.03 MB")
  - TB (terabytes) is the largest unit used even for data sizes greater than 1000 TB.<br>
    (e.g. 10000200 GB => "10000.2 TB")

*`toString()` is reserved for a more technically accurate string representation in bytes (i.e. no rounding, so that two different data sizes can never misleadingly look the same e.g. when logging etc.).*

### 2. Adding

Two data sizes can be added together, resulting in a new data size.

### 3. Parsing

A data size can be parsed from a string.

### 4. Numerical representation

A data size can be "converted" to a numerical representation (up to terabytes) without losing precision.

### 5. Flexible formatting

A data size can be formatted by providing the desired unit symbol (e.g. `dataSize.format("kB"`)), resulting in a string similarly to 1., but in the specified unit and allowing leading zeroes (e.g. 1 byte formatted as megabytes => "0.000001 MB").

### 6. Powers of two

[Powers of two](https://en.wikipedia.org/wiki/Binary_prefix) are supported additionally, e.g. 1 kibibyte (1 KiB) is equal to 1024 bytes, etc.

___

© 2023 Raimund Krämer - Use with attribution.

Links to third party sites are included for convenience only and I am not responsible for their contents.
