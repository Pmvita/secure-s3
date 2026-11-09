# ✅ aws-secure-s3 — TODO

**Spec version:** 2.0 — 2026-09-18 (same version as [`README.md`](./README.md))

**Locked scope:** one data bucket, PAB + AES-256 + HTTPS deny + versioning, CloudTrail opt-in, no committed state.

**Portfolio status:** **code complete; apply pending AWS credentials.** Terraform modules are ready. Live `apply` → verify → `destroy` has not been run on this machine (no configured AWS credentials).

---

- [x] Random bucket name
- [x] Block Public Access (all four)
- [x] BucketOwnerEnforced
- [x] AES-256 default encryption
- [x] HTTPS-only bucket policy
- [x] Versioning
- [x] CloudTrail + log bucket behind `enable_cloudtrail`
- [x] `.gitignore` for tfstate
- [ ] `terraform apply` then `terraform destroy` on a demo account — **pending AWS credentials** (code complete; commands in README)

**Status (2026-11-08):** Terraform modules are ready. Live apply/verify/destroy blocked until `aws sts get-caller-identity` succeeds on the demo machine. *(blocked: no AWS credentials)*

### Exact commands (when credentials exist)

```bash
cd secure-s3
terraform init
terraform plan
terraform apply
# prove HTTPS-only: aws s3 ls s3://$(terraform output -raw data_bucket) --no-sign-request
# should fail closed
terraform destroy
```

Opt-in trail: set `enable_cloudtrail = true` in tfvars, then destroy the same day.

---

*Last updated: 2026-11-08*
