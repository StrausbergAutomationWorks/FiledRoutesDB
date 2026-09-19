# FiledRoutesDB

Filed flight-plan route pairs — callsign to origin and destination — observed
through the U.S. air traffic system.

**A downloadable database, not an API.** Each consumer fetches one small file
and resolves routes locally. There is no endpoint, and none is planned.

## Status

**Nothing is published yet. This repository holds no data.**

Collection is running and the artifact builder is written and tested. The
questions to the FAA that were holding publication have been answered.
Releases will appear here.

## What it will contain

| | |
|---|---|
| Unit | one entry per callsign, listing observed origin/destination pairs |
| Ranking | each pair carries an observation count |
| Identifiers | ICAO airport codes. City and airport names resolve client-side |
| Excluded | positions, tracks, owners, registrants, Mode S addresses |
| Cadence | rebuilt weekly |

Aircraft on the FAA Limiting Aircraft Data Displayed (LADD) list are filtered
out at build time. The build fails closed: no list, an unparseable list, or a
stale list, and nothing is produced.

## Disclaimer

Derived from data obtained through the FAA SWIM Cloud Distribution Service.
**This is not FAA data, is not an official source, and is not endorsed by or
affiliated with the FAA.** Not for operational, air traffic, law enforcement,
or safety-of-life use.

Availability depends on upstream services and may be interrupted without
notice.

## Licence

MIT. See `LICENSE`.
