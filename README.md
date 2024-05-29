# Elastic Stack Docker Compose Configuration

This Docker Compose configuration sets up an Elastic Stack environment, including Elasticsearch, Kibana, Logstash, Metricbeat, Filebeat, and Suricata, using the specified versions.

## TL;DR

```bash	
mv example.env .env && docker-compose up -d
```
https://localhost:5601

**Username:** elastic

**Password:** Megapassword

## Prerequisites

Before running this Docker Compose setup, ensure you have Docker installed on your system.

## Getting Started

To get started, follow these steps:

1. Clone this repository to your local machine.
2. Create a `.env` file in the root directory of the cloned repository and define the following environment variables:
   - `STACK_VERSION`: The version of the Elastic Stack components.
   - `ES_PORT`: The port for Elasticsearch.
   - `KIBANA_PORT`: The port for Kibana.
   - `CLUSTER_NAME`: The name of the Elasticsearch cluster.
   - `ELASTIC_PASSWORD`: The password for the Elasticsearch and Kibana users.
   - `LICENSE`: The type of license for X-Pack.
   - `ES_MEM_LIMIT`: The memory limit for Elasticsearch.
   - `KB_MEM_LIMIT`: The memory limit for Kibana.
   - `ENCRYPTION_KEY`: The encryption key for X-Pack.
3. Run `docker-compose up -d` to start the Elastic Stack containers.

## Services

The Docker Compose configuration defines the following services:

- **setup**: Initializes the Elasticsearch environment, generates SSL certificates, sets file permissions, and waits for Elasticsearch availability.
- **es01**: Elasticsearch service with SSL enabled and X-Pack security configured.
- **kibana**: Kibana service configured to connect to Elasticsearch securely.
- **logstash01**: Logstash service configured to send data to Elasticsearch.
- **metricbeat01**: Metricbeat service for collecting metrics from the host and services.
- **filebeat01**: Filebeat service for shipping log files to Elasticsearch.
- **suricata**: Suricata service for intrusion detection, integrated with Elasticsearch.

## Configuration

- SSL certificates are stored in volumes for secure communication.
- Each service depends on the health of the Elasticsearch service.
- Services are configured to communicate securely over HTTPS.

## Usage

Once the services are up and running, you can access Kibana at `https://localhost:<KIBANA_PORT>` and authenticate using the credentials configured in the `.env` file.

There are 2 folders to ingest data into the Elastic Stack:

- **filebeat_ingest_data**: Contains log files to be ingested by Filebeat. By default, suricata logs are sent to this folder.
- **logstash_ingest_data**: Contains log files to be ingested by Logstash.

## Additional Information

For more information on configuring and customizing the Elastic Stack components, refer to the official documentation:

- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [Kibana Documentation](https://www.elastic.co/guide/en/kibana/current/index.html)
- [Logstash Documentation](https://www.elastic.co/guide/en/logstash/current/index.html)
- [Beats Documentation](https://www.elastic.co/guide/en/beats/libbeat/current/index.html)
- [Suricata Documentation](https://suricata.readthedocs.io/en/latest/)
