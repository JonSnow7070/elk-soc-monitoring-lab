# Configuration Templates

This directory contains example configuration templates for the ELK-based SOC monitoring lab.

## Files

### `filebeat.yml.example`

An example Filebeat configuration demonstrating how to collect Linux log files and forward events to Elasticsearch.

Before using it, configure the Elasticsearch server address and the appropriate authentication credentials for your environment.

### `kibana.yml.example`

An example Kibana configuration showing the server settings, Elasticsearch connection, authentication settings, and encrypted saved objects configuration.

Replace the example placeholders with values appropriate for your own lab before using the configuration.

## Usage

1. Review the relevant example file.
2. Create a separate working configuration on your own machine.
3. Replace placeholders with your environment-specific values.
4. Validate the configuration before restarting the relevant service.

## Security Considerations

- Never commit real passwords, API keys, tokens, or encryption keys.
- Do not upload production configuration files containing secrets.
- Use placeholders in public examples.
- Protect local configuration files and restrict access to credentials.

These files are educational examples and may require adjustments for different Elastic Stack versions and environments.

