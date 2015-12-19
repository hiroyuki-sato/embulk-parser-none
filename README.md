# None parser plugin for Embulk

Embulk parser plugin not to parse at all

## Install

```
$ embulk gem install embulk-parser-none
```

## Overview

* **Plugin type**: parser
* **Guess supported**: no

## Configuration

- **message_key**: A column name which this plugin outputs (string, default: "message")

## Example

```yaml
in:
  type: file
  path_prefix: example.txt
  parser:
    type: none
    message_key: message
```

Assume the input file (example.txt) is as following:

```
foo bar baz
foo bar baz
```

then this plugin treats as:

```
+----------------+
| message:string |
+----------------+
| foo bar baz    |
| foo bar baz    |
+----------------+
```

To recover a file, you may use csv formatter as:

```
out:
  type: file
  path_prefix: example.txt
  sequence_format: ""
  file_ext: .out
  formatter:
    type: csv
    quote_policy: NONE
```

## ChangeLOG

[CHANGELOG.md](CHANGELOG.md)

## Development

Run example:

```
$ ./gradlew classpath
$ embulk run -I lib example.yml
```

Run test:

```
$ ./gradlew test
```

Release gem:

```
$ ./gradlew gemPush
```
