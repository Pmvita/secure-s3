

# aws-secure-s3

### Locked-down S3 from Terraform - Block Public Access, AES-256, HTTPS-only

v2 of [Pmvita/aws-secure-s3](https://github.com/Pmvita/aws-secure-s3). The old repo was a bash script with hardcoded bucket names and an account ID in the README. This lab is **Terraform**, **random bucket names**, **Windows-friendly**, and **CloudTrail off by default**.



---

**Spec version:** 2.0 — 2026-09-18 (same version as `[TODO.md](./TODO.md)`)

## Overview

Creates one data bucket:

- Block Public Access (all four flags)
- BucketOwnerEnforced (no ACLs)
- AES-256 default encryption
- Versioning
- Bucket policy deny if `aws:SecureTransport` is false
- `force_destroy` so `terraform destroy` actually finishes

CloudTrail is **opt-in**. A trail plus a log bucket is extra moving parts and not required to prove the hardening.

## Locked scope

- One data bucket, random suffix
- No KMS CMK (AES-256 is enough and $0)
- No public `Principal: "*"` GetBucketAcl (that was in v1)
- No committed state
- Destroy after the demo



## Status

**Code complete.** Modules harden one data bucket (PAB, AES-256, HTTPS-only, versioning). Live `terraform apply` / `destroy` is **pending AWS credentials** on the demo machine — do not claim a live bucket until you have run the steps below.

## Getting started

```bash
terraform init
terraform plan
terraform apply
# prove HTTPS-only: aws s3 ls s3://$(terraform output -raw data_bucket) --no-sign-request
# should fail closed
terraform destroy
```

Opt-in trail:

```hcl
enable_cloudtrail = true
```

Destroy the same day if you enable CloudTrail.



## v1 → v2


| v1                                 | v2                                |
| ---------------------------------- | --------------------------------- |
| `secure-s3-pierre` hardcoded       | random suffix                     |
| Bash / AWS CLI                     | Terraform                         |
| CloudTrail always                  | `enable_cloudtrail = false`       |
| Account ID pasted in README        | `data.aws_caller_identity`        |
| `Principal: "*"` on log bucket ACL | CloudTrail service principal only |




## License

MIT. See [LICENSE](./LICENSE).