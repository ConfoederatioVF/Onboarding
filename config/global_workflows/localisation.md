---
description: Enforces localisation for the current project scope.
---

Make sure the following locales are supported: EN-GB, DE, FR.

EN-GB is the default fallback and ground truth for which other supported languages should be machine-translated for. Ensure the following is true of your project:
1. All user-facing human-readable strings are localised.
2. All localisation lives in the `/localisation/` folder as a series of JSON/JSON5 files.
3. Delimiters for numbers/values are given as £1£, £2£, £n£, ...
4. There is a language setting somewhere in the project that allows for end users to change their specified language from the machine-detected locale.