# Students — DJANGO_HEALTH_CHECK

**Project:** DJANGO_HEALTH_CHECK  
**Category:** MEDICAL_HEALTH  
**Upstream:** https://github.com/labd/django-healthchecks  
**Pinned commit:** `37e548e8ee2bf15b1afb98f078ee54ec63f1e621`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `55e06224af5d7f99de85309d3e781c1291177e4e81711d35f59b5f6fc61ed429`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `37e548e8ee2bf15b1afb98f078ee54ec63f1e621`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `55e06224af5d7f99de85309d3e781c1291177e4e81711d35f59b5f6fc61ed429`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
