- Environment: Windows/PowerShell, Node v24.19.0, npm 11.19.0, @nitrosend/cli 0.3.8. From the test directory I installed with `node ../package-tools/node_modules/npm/bin/npm-cli.js install --ignore-scripts --no-audit --no-fund --save-exact @nitrosend/cli@0.3.8 @nitrosend/sdk@0.11.2 typescript @types/node`; npm was already available locally.

- Authentication/setup: the operator registered and provided a dedicated API key; I supplied it through NITROSEND_API_KEY. `status --json` supplied the brand SID. POST `/v1/my/brands/<sid>/prepare_sending` with `{"subdomain":"kgway-client-check"}` returned ready; `mcp tools call nitro_configure_account` set the kgway sender. No campaign, contact import or postal address was used.

- Commands used the installed `node node_modules/@nitrosend/cli/dist/index.js`: `--version`, `--help`, `status --json`, `mcp tools list --json`, then `send --to proof@dogfood.nitrosend.net --subject "CSV publication guide: CLI delivery check" --body "kgway is checking one transactional notification for an original CSV publication guide. This CLI delivery check needs no reply." --idempotency-key kgway-cli-publication-check-20261020-v1 --json`, first with `--dry-run`. A Node wrapper passed exact argv to avoid shell re-quoting; [run-results.json](./run-results.json) records it.

- Timing: 9.44 minutes from install start to provider sent status, including mobile registration/key handoff. That handoff was the slowest step; this is not an unattended setup-time benchmark.

- Actual result: dry-run valid; live command exited 0 and returned queued. GET `/v1/my/messages/<id>` subsequently returned sent at 2026-10-20T07:38:42.27Z, with no failure code. Recipient inbox arrival was not inferred from that status.

- No product defect found in version/help, tool-schema discovery, explicit sender preparation, dry-run and one real send. I checked the CLI README and official install/reference pages. One change: put the explicit-subdomain first-send path ahead of paid-upgrade recommendations in status output for a free account with unused allowance.
