# FiledRoutesDB

Filed flight-plan route pairs, callsign to origin and destination, observed
through the U.S. air traffic system.

**A downloadable database, not an API.** Each consumer fetches one small file
and resolves routes locally. There is no endpoint, and none is planned.

## Download

The current file is attached to the [`data` release](https://github.com/StrausbergAutomationWorks/FiledRoutesDB/releases/tag/data):

```
https://github.com/StrausbergAutomationWorks/FiledRoutesDB/releases/download/data/filedroutesdb.json.gz
https://github.com/StrausbergAutomationWorks/FiledRoutesDB/releases/download/data/SHA256SUMS
```

The file is rebuilt **daily**. Only the current file is published; each build
replaces the previous one, and superseded files are not kept here.

## Format

One gzipped JSON document. Top-level fields:

| Field | Meaning |
|---|---|
| `format` | `filedroutesdb/1` |
| `built`, `expires` | UTC timestamps. **Do not use the file after `expires`** (10 days after it was built). |
| `ladd_applied` | Date of the FAA LADD list this build was filtered against. A file without it must be refused. |
| `ladd_entries`, `ladd_suppressed` | Size of that list, and how many identifiers the build suppressed |
| `collection_start` | First day of collection behind the file |
| `min_observations`, `leg_dormant_days` | Build thresholds, below |
| `attribution`, `licence`, `licence_url`, `home` | Provenance and terms, below |
| `routes` | The data |

`routes` maps a callsign to:

| Key | Meaning |
|---|---|
| `u` | user category (`COMMERCIAL`, `CARGO`, `GENERAL AVIATION`, `AIR TAXI`, `MILITARY`, `OTHER`, `UNKNOWN`) |
| `a` | aircraft category (`JET`, `TURBO`, `PISTON`, `OTHER`) |
| `s` | last time the callsign was seen, epoch seconds UTC |
| `l` | its legs, most observed first: `{"r": "ORIGIN-DESTINATION", "n": observations}` |

Airports are ICAO codes. Names and coordinates are left to the consumer.

**A callsign often has more than one leg.** Most are one city pair flown in
both directions; some are genuine multi-leg flight numbers. The observation
count ranks them, but the right leg for a given aircraft depends on where it
is, which only the consumer knows. Do not assume the first leg is the one
being flown.

### Build rules

* A leg needs at least `min_observations` observations.
* A leg not seen for `leg_dormant_days` is left out when the same callsign has
  flown another leg within that time. This drops routes a flight number no
  longer flies. A callsign whose legs are all quiet keeps them.
* Positions, tracks, times, owners, registrants and Mode S addresses are not
  published.

## LADD

Aircraft on the FAA Limiting Aircraft Data Displayed (LADD) list are excluded
from every build, including all historical data for them. The filter is
applied to the whole collection on every build, so an aircraft added to the
list disappears from the next file.

An aircraft that leaves the list is published again only when the FAA's
removal file names it. One that leaves without a removal entry stays
excluded.

The build fails closed: no list, an unparseable list, or a list more than
seven days old, and nothing is produced.

## Disclaimer

Derived from data obtained through the FAA SWIM Cloud Distribution Service.
**This is not FAA data, is not an official source, and is not endorsed by or
affiliated with the FAA.** Not for operational, air traffic, law enforcement,
or safety-of-life use.

Availability depends on upstream services and may be interrupted without
notice.

## Licence

* **Data** (the release files): [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
  See `DATA_LICENSE.md`. Attribution must name FiledRoutesDB and carry the
  disclaimer above.
* **Code** in this repository: MIT. See `LICENSE`.
