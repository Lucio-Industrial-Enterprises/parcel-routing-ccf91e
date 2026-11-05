# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a shipping quote
in dollars. Zones are `local` and `regional`; weights must be positive.

| Service    | Local base | Regional base | Express surcharge |
|------------|-----------|---------------|-------------------|
| `standard` | $5.00     | $8.00         | —                 |
| `express`  | $5.00     | $8.00         | +$7.00            |

Rate formula: `base + 1.5 × weight_kg [+ surcharge]`

Unknown zones or service levels raise `ValueError`.

### CLI

```
python -m warehouse.cli <weight_kg> <zone> [--service {standard,express}]
```

Examples:

```
# Standard quote for a 2 kg parcel in the local zone → $8.00
python -m warehouse.cli 2 local

# Express quote for the same parcel → $15.00
python -m warehouse.cli 2 local --service express
```
