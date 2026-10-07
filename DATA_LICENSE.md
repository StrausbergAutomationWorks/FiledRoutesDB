# Data licence

The data files published in this repository's releases (`filedroutesdb.json.gz`
and its checksum file) are licensed under the
**Creative Commons Attribution 4.0 International licence (CC BY 4.0)**:
https://creativecommons.org/licenses/by/4.0/

Copyright (c) 2026 Lee E. Strausberg and StrausbergAutomationWorks.

## Attribution

Attribution must:

1. name **FiledRoutesDB** and link to
   https://github.com/StrausbergAutomationWorks/FiledRoutesDB, and
2. carry this notice unaltered:

   > Derived from data obtained through the FAA SWIM Cloud Distribution Service.
   > This is not FAA data, is not an official source, and is not endorsed by or
   > affiliated with the FAA. Not for operational, air traffic, law enforcement,
   > or safety-of-life use.

## Expiry and the LADD list

Each file states an `expires` time and the FAA LADD list it was filtered
against (`ladd_applied`). Aircraft are added to that list every week. Using a
file after it expires, or redistributing it after that, can display aircraft
whose owners have asked not to be displayed. Fetch the current file instead.

The software in this repository is licensed separately, under MIT (`LICENSE`).
