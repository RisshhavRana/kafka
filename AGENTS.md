# AGENTS.md

## Setup

- No `requirements.txt`. Required packages: `confluent-kafka`, `pyspark`.
- Environment variables required at runtime:
  - `KAFKA_API_KEY` — Confluent Cloud API key (used as SASL username)
  - `KAFKA_API_SECRET` — Confluent Cloud API secret (used as SASL password)
- Bootstrap server is hardcoded to `pkc-9q8rv.ap-south-2.aws.confluent.cloud:9092` in all scripts.

## Architecture

- `Producer.py` — sends 10 JSON messages to `my_first_topic`, uses `__name__ == "__main__"` guard.
- `Consumer.py` — polls `my_first_topic` with manual offset commit; runs in infinite loop (Ctrl+C to stop).
- `Spark Structured Streaming with Databricks.py` — Spark streaming read from same topic; user must define `spark` session externally (e.g. in Databricks notebook). JAAS config uses `<USERNAME>`/`<PASSWORD>` placeholders — replace before use.

## Conventions

- Confluent Cloud broker: SASL_SSL with PLAIN mechanism. Do not change auth protocol unless switching broker.
- Kafka topic is `my_first_topic` across all scripts — changing it requires updating all three files.