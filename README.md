# MAP publication check

An original Mail Action Protocol 0.3 description for publishing the accompanying CSV editing note, with actual CLI validation evidence.

- `description.json`: valid original description; the recipient is synthetic and no approval is executed.
- `article.md`: the author's content, whose UTF-8 bytes are identified by the content digest.
- `report.md`: concise test report.
- `run-results.json`: actual commands, UTC timestamps, exit codes and output from the run.
- `description-broken.json`: the single-field negative fixture.

To check the two fixtures in a directory with Node 22 or newer, first download the official [Publication Approval contract](https://mailschema.org/artifacts/map-0.3/contracts/publication-approval-0.1.json) and save it as `publication-contract.json`. The contract digest is pinned inside the description.

```sh
npm install mailschema@0.3.2
npx mailschema@0.3.2 description description.json --contract publication-contract.json
npx mailschema@0.3.2 description description-broken.json --contract publication-contract.json
```

The second check should exit 1 because a restricted destination requires audience metadata. This repository demonstrates document checks only; it is not a live MAP service binding, authentication implementation or approval system.

Contract source: https://mailschema.org/artifacts/map-0.3/contracts/publication-approval-0.1.json. The original guide, request and report were prepared by the account owner's authorized OpenAI Codex assistant.
