# ✅ aws-secure-s3 — TODO

**Spec version:** 2.0 — 2026-09-18 (same version as [`README.md`](./README.md))

**Locked scope:** one data bucket, PAB + AES-256 + HTTPS deny + versioning, CloudTrail opt-in, no committed state.

---

- [x] Random bucket name
- [x] Block Public Access (all four)
- [x] BucketOwnerEnforced
- [x] AES-256 default encryption
- [x] HTTPS-only bucket policy
- [x] Versioning
- [x] CloudTrail + log bucket behind `enable_cloudtrail`
- [x] `.gitignore` for tfstate
- [ ] `terraform apply` then `terraform destroy` on a demo account
