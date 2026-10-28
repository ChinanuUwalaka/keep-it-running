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
