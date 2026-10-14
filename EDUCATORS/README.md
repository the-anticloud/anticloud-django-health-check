# Educators — DJANGO_HEALTH_CHECK

**Project:** DJANGO_HEALTH_CHECK  
**Category:** MEDICAL_HEALTH  
**Upstream:** https://github.com/labd/django-healthchecks  
**Pinned commit:** `37e548e8ee2bf15b1afb98f078ee54ec63f1e621`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `55e06224af5d7f99de85309d3e781c1291177e4e81711d35f59b5f6fc61ed429`  
**Date:** October 2026

## Teaching with DJANGO_HEALTH_CHECK

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `55e06224af5d7f99de85309d3e781c1291177e4e81711d35f59b5f6fc61ed429` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.
