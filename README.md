# debugexpress-proof

Evidence repo for DeBugExpress's autonomous detect → fix → prove → ship →
rollback pipeline.

This ran against a disposable test application built specifically to
validate the pipeline end-to-end — not live production traffic. That's
what made it possible to safely trigger the review-rejection and rollback
scenarios for real, on purpose, without risking a real user-facing app.

## What's in here

- **`01-detect-fix-prove/`** — a real bug, detected automatically,
  triaged, fixed, and shipped as a real pull request that a human
  approved and merged. Includes the real fix diff and the real PR body.
- **`02-review-rejection/`** — proof the review step isn't a rubber
  stamp: a generated fix that solved the bug anyway got rejected for a
  real security concern (logging sensitive request data) before it ever
  reached a pull request.
- **`03-rollback/`** — the bug was deliberately reintroduced right after
  a fix deployed, to prove the one thing every automated-fix tool claims
  and few prove: it noticed, and reverted itself automatically, via a new
  commit — never a force-push or rewritten history.
- **`04-notification/`** — the real email that arrived when a fix
  deployed, not a design mockup.

## What's honestly missing, and why

The AI-generated regression test's source code, and the raw console
output from running it, aren't in this repo. They only ever existed in a
transient verification workspace on the server during that one run —
never committed to git, never saved to a database, nothing left to pull
after the fact. Where that step matters to a section's story, the real,
contemporaneous PR text describing it (generated and posted at the time,
not reconstructed later) is included instead. Nothing in this repo was
rewritten to look more complete than what's actually still real and
recoverable.

## What's not in here, on purpose

This repo contains no DeBugExpress application code — no triage/fix/review
pipeline source, no server code, no deployment configuration, no API
integration code. It's evidence, not a working copy of the product, and it
can't be run, deployed, or connected to anything real.

The actual product lives at [getdebugexpress.com](https://getdebugexpress.com).
