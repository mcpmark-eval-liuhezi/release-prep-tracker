# Release Checklist

This document tracks the rollout of the upcoming release end to end, covering preparation, deployment, verification, and rollback.

## 1. Pre-release preparation

- [ ] Confirm the release version number and tag name.
- [ ] Freeze feature work; allow only fixes and documentation.
- [ ] Dependency audit complete (see the "Dependency audit" sub-issue).
- [ ] Docs refresh complete (see the "Docs refresh" sub-issue).
- [ ] Smoke test matrix executed and results recorded (see the "Smoke test matrix" sub-issue).

## 2. Rollout steps

1. Cut the release branch and generate the release build artifacts.
2. Run the full automated test suite against the build artifacts.
3. Publish the artifacts to the staging environment.
4. Run the smoke test matrix against staging and confirm all critical paths pass.
5. Notify the release channel that rollout is beginning, and confirm an operator is on call.
6. Promote the staging build to production.
7. Announce the release in the changelog and release notes.

## 3. Verification

- [ ] Smoke test matrix passes on production.
- [ ] Error rates and key dashboards are within normal ranges for at least 30 minutes.
- [ ] No critical or high severity incidents reported post-deployment.
- [ ] Release notes and documentation are published and accurate.

## 4. Rollback plan

**Trigger criteria:** Roll back immediately if any of the following occur:

- A critical or high severity failure in a core user path.
- Error rate exceeds the agreed threshold (2x baseline) for more than 5 minutes.
- Data integrity or security issue discovered.

**Rollback procedure:**

1. Declare the rollback in the release channel and stop further rollout steps.
2. Revert the production deployment to the previously tagged stable release.
3. Re-run the smoke test matrix against the restored version to confirm health.
4. Confirm monitoring dashboards return to baseline.
5. Post a follow-up in the release channel documenting the cause and the fix plan.

**Verification after rollback:**

- [ ] Previous stable version is confirmed live in production.
- [ ] Smoke test matrix passes on the restored version.
- [ ] Incident ticket created with root cause analysis and corrective actions.

## 5. Sign-off

- [ ] Release lead confirms all verification items pass.
- [ ] Checklist reviewed by a second reviewer before merge.
