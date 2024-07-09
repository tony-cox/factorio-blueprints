# factorio-blueprints
This repo is just to store all of my Factorio blueprints.  They are considered open source under the MIT license - free for anyone to take, copy, modify and use.

## Encoding/Decoding
Note that blueprints here are decoded to JSON before being source controlled.  This assists greatly with viewing changes, and saves from having a separate description attached to each one, as the descriptions can simply be read within the JSON.  It does, however, add some overhead to being able to use them.  For reference, see [Blueprint string format](https://wiki.factorio.com/Blueprint_string_format).

### Prerequisites
You will need pigz (for zlib compression) and jq (json processing) installed via your favourite package manager (apt on ubuntu).

`apt update && apt install pigz jq -y`

### Decoding
Decode a blueprint stored in **raw** and print it to console with:

`cut -c2- raw | base64 -d | pigz -cd | jq`

Decode a blueprint and save it to a file named **pretty**:

`cut -c2- raw | base64 -d | pigz -cd | jq > pretty`

### Encoding
To encode the **pretty** file back to **raw**:

`cat pretty | { printf 0; jq -c . | pigz -9 | base64 -w0; } > raw`
