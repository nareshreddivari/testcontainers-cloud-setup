# Testcontainers Cloud action

This action downloads and runs the agent. Either `token` parameter or `TC_CLOUD_TOKEN` environment variable is required.

## Example usage

```yaml
name: Java CI with Maven

on:
  push:
    branches: [ main ]

jobs:
  build:
    name: "Run checks"
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v3

      - uses: actions/setup-java@v3
        with:
          java-version: '8.0.345'
          distribution: temurin
          
      # Setup Testcontainers Cloud Client right before your Testcontainers tests
      - name: Setup Testcontainers Cloud Client
        uses: atomicjar/testcontainers-cloud-setup-action@v1
        with:
          token: ${{ secrets.TC_CLOUD_TOKEN }}
          
      - name: Build with Maven
        run: mvn -V -B verify
```

## Configurable parameters

- `token` (__required__):  `secret-string` - service account token for Testcontainers Cloud
- `version` (_optional_):  `latest` (default) - Testcontainers Cloud binary version
- `wait` (_optional_):  `true` (default) /`false` - if action should wait until agent successfully connects to Testcontainers Cloud in advance
- `args` (_optional_): `string` - flags/arguments of the agent to pass as is. Consult with the knowledge base to find out more about possible options.
- `logfile` (_optional_): `string` - file to write the agent output instead of the standard out.