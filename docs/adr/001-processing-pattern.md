# ADR 001: Choose Kappa Processing Architecture

## Status
Accepted

Date: 2026-11-20

## Context
Our launch customer is Alpine Outdoor (SHP01).

The platform must meet these requirements:
- Freshness: Shipment updates within 15 minutes.
- Reliability: At least 55% on-time shipments on each lane.
- Budget: Maximum $20 per month.

BigQuery analysis of 156 shipments shows two lanes below target:
- Ningbo to Hamburg: 51.2% on time, average delay 42.7 hours.
- Busan to Long Beach: 52.8% on time, average delay 38.3 hours.

The platform needs timely shipment monitoring and low-cost historical analysis.

## Options considered
1. **Lambda architecture:** Uses separate live and batch processing pipelines. It supports different workloads but increases maintenance and complexity.
2. **Kappa architecture:** Uses one main event-processing pipeline, with stored events available for reprocessing. It reduces duplicated processing logic.

## Decision
We chose **Kappa architecture** with scheduled micro-batch ingestion every 5 minutes.

This design uses Cloud Storage for raw events, Cloud Run for ingestion, and BigQuery for shipment monitoring and historical analysis.

Kappa is preferred because it is simpler to maintain and better suited to Alpine Outdoor's small monthly budget. The 5-minute schedule is intended to support the 15-minute freshness requirement.

## Consequences
- **Cost:** Target under $20 per month. Actual cost must be estimated and monitored.
- **Freshness:** Ingestion every 5 minutes, aiming for end-to-end updates within 15 minutes.
- **Complexity:** One primary processing pipeline reduces duplication but still requires scheduling, monitoring, and error handling.
- **What gets harder:** Reprocessing old events and handling late shipment updates require additional logic.