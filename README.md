# Keep It Running — DevOps Capstone 2

## Overview
A local observability stack for monitoring service health and collecting container logs.

## Technology Stack
- Prometheus — metrics collection and querying
- Grafana — monitoring dashboards and visualization
- Loki — log aggregation
- Grafana Alloy — Docker container log collection

## Prerequisites
- Docker Engine
- Docker Compose

## Start the Stack
Run: `docker compose up -d`
Then check: `docker compose ps`

## Local Endpoints
| Service | URL |
|---|---|
| Grafana | http://localhost:13000 |
| Prometheus | http://localhost:19090 |
| Loki | http://localhost:13100 |
| Alloy | http://localhost:12345 |

## Health Checks
- Prometheus: `curl http://127.0.0.1:19090/-/healthy`
- Loki: `curl http://127.0.0.1:13100/ready`
- Grafana: `curl http://127.0.0.1:13000/api/health`

## Configuration
- `compose.yaml` — service definitions
- `monitoring/prometheus/prometheus.yml` — Prometheus configuration
- `logging/loki/loki-config.yaml` — Loki configuration
- `logging/alloy/config.alloy` — container log collection

## Current Scope
This submission contains the observability foundation. Additional tracing, alerting, application instrumentation, and incident-response evidence should only be claimed after implementation and testing.

## Extended Observability Components

The optional `compose.remaining.yaml` adds Alertmanager, Jaeger, the OpenTelemetry Collector, and Fluent Bit without replacing the base Compose file.

Start the extended stack with:

`docker compose -f compose.yaml -f compose.remaining.yaml up -d`

Local endpoints:
- Alertmanager: http://localhost:19093
- Jaeger tracing UI: http://localhost:16686
- OpenTelemetry OTLP/gRPC receiver: localhost:14317
- OpenTelemetry OTLP/HTTP receiver: http://localhost:14318

Prometheus alert rules are defined in `monitoring/prometheus/alerts.yml`.
Alertmanager routing is configured in `alerts/alertmanager.yml`.
The OpenTelemetry Collector pipeline is in `tracing/otel-collector.yml`.
Fluent Bit configuration and demonstration logs are in `logging/fluent-bit/`.

The Fluent Bit example reads only the included sample logs and writes parsed events to its stdout output. It is a demonstration, not a claim that Fluent Bit forwards logs to Loki. Existing Alloy configuration is responsible for collecting the selected capstone containers' Docker logs.

Alertmanager currently has no external notification integration configured. The Collector requires an instrumented application or trace generator to send spans before Jaeger can display application traces. Confirm these behaviors before describing them as fully tested.
