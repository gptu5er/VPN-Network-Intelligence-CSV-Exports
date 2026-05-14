# VPN Network Intelligence CSV Exports

This repository publishes two CSV files generated from a VPN infrastructure collector:

- `asn_multi_provider.csv`
- `vpn-ip.csv`

The files are intended for security research, abuse prevention, fraud detection, traffic analysis, and network intelligence workflows.

## Files

### `asn_multi_provider.csv`

This file lists autonomous systems where more than one VPN provider was observed.

Columns:

| Column | Description |
|---|---|
| `ASN` | Autonomous System Number. |
| `Org` | ASN organization name from the enrichment source. |
| `IPs` | Number of observed VPN IPs in this ASN. |
| `Providers` | Number of distinct VPN providers observed in this ASN. |
| `Names` | Comma-separated provider names observed in this ASN. |

Example:

```csv
ASN,Org,IPs,Providers,Names
212238,CDNEXT,"5,263",22,"Astrill, CactusVPN, CyberGhost, ExpressVPN, Hide.me"
```

### `vpn-ip.csv`

This file lists IPv4 `/24` network ranges where VPN provider IPs were observed.

Columns:

| Column | Description |
|---|---|
| `range` | IPv4 `/24` range containing one or more observed VPN provider IPs. |

Example:

```csv
range
1.2.3.0/24
5.6.7.0/24
```

## Notes

- `asn_multi_provider.csv` is ASN-level data. It does not mean every IP in an ASN belongs to every listed provider.
- `vpn-ip.csv` is range-level data. A listed `/24` means at least one observed VPN IP was found inside that range.
- These datasets are indicators, not final blocking decisions. Consumers should combine them with their own logs, risk scoring, and allow/deny policies.
- The data can change as VPN providers rotate infrastructure.

## Suggested Use

- Identify hosting networks shared by multiple VPN providers.
- Build ASN-level risk signals for fraud and abuse systems.
- Track IPv4 ranges where VPN infrastructure has been observed.
- Enrich logs or events with VPN infrastructure context.
