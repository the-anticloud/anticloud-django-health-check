# Ethics — DJANGO_HEALTH_CHECK

**Project:** DJANGO_HEALTH_CHECK  
**Category:** MEDICAL_HEALTH  
**Upstream:** https://github.com/labd/django-healthchecks  
**Pinned commit:** `37e548e8ee2bf15b1afb98f078ee54ec63f1e621`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `55e06224af5d7f99de85309d3e781c1291177e4e81711d35f59b5f6fc61ed429`  
**Date:** October 2026

## Position

DJANGO_HEALTH_CHECK is packaged for offline deployment with a verifiable audit trail. The
ethical questions this raises are answered by making the system's behaviour
checkable rather than by policy statements.

## The four commitments

1. **No hidden egress.** The deployment has no external API dependency; this is
   testable by running it with the network disconnected.
2. **Attributable output.** Every artifact is recorded in a hash chain, so what
   the system produced can be reconstructed.
3. **Operator control.** The institution owns the hardware and the keys.
4. **Refusal to overclaim.** Where a certification is not held, the project says
   so rather than implying it.

## Dual use

This project is packaged for civilian and public-sector deployment. Where an
upstream has dual-use characteristics, the licence gate and the reference-only
marking in `BENCH.json` record that.
