# MAP 0.3 publication-description run

- I authored a publication request for my CSV text-identifier guide, rather than copying a Registry example. The recipient is deliberately synthetic (`reviewer@example.invalid`). This checks a document, not a GitHub MAP implementation, an authenticated email, or an executed approval. `content.digest` identifies the exact UTF-8 bytes of `article.md`.
- Runtime: Node v24.19.0; npm 11.19.0; mailschema 0.3.2; Windows. `node` below denotes the bundled Node executable. From the workspace I ran `node revenue-work/package-tools/node_modules/npm/bin/npm-cli.js install --prefix revenue-work/map-check mailschema@0.3.2 --ignore-scripts --no-audit --no-fund`.
- From `revenue-work/map-check` I ran `node build-description.mjs`, then `node ../package-tools/node_modules/npm/bin/npx-cli.js --no-install mailschema@0.3.2 description description.json --contract publication-contract.json`. The test runner repeated that exact CLI command for valid, broken and restored inputs. Setup-to-first-logged-pass was 2.46 minutes, an upper bound: the first successful interactive pass preceded the logged run.
- I changed only `details.destinations[0].visibility` from `public` to `restricted`, leaving out `audience`. Exit 1 printed exactly:

  ```text
  /details/destinations/0: must have required property 'audience'
  /details/destinations/0: must match "then" schema
  ```

- Restoring `public` restored the original bytes and digest. The CLI's second line matched `digest(parseDescription(bytes))`; reversing top-level key order preserved that digest. See `run-results.json` for timestamps and outputs.
- Slowest step: assembling the required envelope from the core schema and obtaining local npm. An initial npm path lookup failed before npm was installed locally.
- No package defect found in these checks. The [README](https://github.com/mailschema/javascript/blob/d6d7ab2585340daf204cc531b7ca53e838ded8a9/README.md) correctly describes exit codes and digest lines; the [Publication Approval contract](https://mailschema.org/artifacts/map-0.3/contracts/publication-approval-0.1.json) requires an audience for restricted destinations. I would add a concise required-envelope walkthrough beside the CLI example. Prepared and executed with OpenAI Codex assistance.
