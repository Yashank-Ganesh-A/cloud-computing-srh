# Session 03 — Shipment Reliability Metrics

**Student:** Yashank Akula
**Launch Customer:** Alpine Outdoor
**Shipper ID:** SHP01
**Transport Mode:** OCEAN

## 1. Customer Requirements

- Freshness target: 15 minutes
- Reliability target: 55% on-time shipments on every lane
- Monthly cloud budget: $20

A shipment is on time if it arrives no more than 24 hours after its planned arrival.

## 2. BigQuery Results

| Shipping Lane | Shipments | Average Delay (Hours) | On-Time Rate | Target | Status |
|---|---:|---:|---:|---:|---|
| CNNGB → DEHAM (Asia-North Europe) | 43 | 42.7 | 51.2% | 55% | FAIL |
| KRPUS → USLGB (Transpacific) | 36 | 38.3 | 52.8% | 55% | FAIL |
| NLRTM → USHOU (Transatlantic) | 41 | 50.0 | 58.5% | 55% | PASS |
| GBFXT → CNSHA (North Europe-Asia) | 36 | 47.7 | 72.2% | 55% | PASS |

Total shipments analyzed: 156.

## 3. Analysis

Two shipping lanes fail the 55% reliability target:

1. Ningbo to Hamburg: 51.2%, which is 3.8 percentage points below target.
2. Busan to Long Beach: 52.8%, which is 2.2 percentage points below target.

The Rotterdam to Houston and Felixstowe to Shanghai lanes meet the target.

## 4. Recommendations

- Prioritize monitoring the two underperforming lanes.
- Investigate which carriers serve these lanes and their delay performance.
- Keep operational shipment information within the 15-minute freshness target.
- Use scheduled analysis for historical reliability reports.
- Design cloud resources to stay within the $20 monthly budget.

## 5. Conclusion

Alpine Outdoor meets its on-time reliability target on two of four shipping lanes. Ningbo to Hamburg and Busan to Long Beach require further investigation and monitoring.
