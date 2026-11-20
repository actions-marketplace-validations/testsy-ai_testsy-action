# Testsy

Testsy runs QA tests written in plain English on websites and on iOS and Android apps, and returns a verdict for every check with its evidence: a replay, video, the values it saw, console and network.

Documentation: https://testsy.dev/docs/mcp/ · Sign up: https://app.testsy.dev

## Use it in a workflow

```yaml
- uses: testsy-ai/testsy-action@v1
  with:
    api-key: ${{ secrets.TESTSY_AI_API_KEY }}
    project: p_yourproject
```

The step starts the project's saved tests, waits for them and fails the job when a test fails. Each test prints its verdict with a link to the run and a watch link that opens without signing in. A JUnit report is written to `testsy-junit.xml`.

- `api-key` (required): a workspace API key from https://app.testsy.dev, stored as a repository secret.
- `project` or `tests`: a project id, or a comma-separated list of saved test ids.
- `target-url`: start website tests at a preview or staging deploy of the same site.
- `build`: an APK or zipped iOS Simulator app (a path, an https link or a build id) for app tests.
- `fail-on`: which results fail the job; for a strict release gate use `failed,error,blocked,inconclusive,cancelled`.

All inputs are in action.yml. Pin a commit SHA in production. The action bundles its own Node CLI (Node 22 or later, present on GitHub-hosted runners); the same CLI runs anywhere: `node bin/testsy.mjs run --project p_yourproject --junit testsy-junit.xml` with TESTSY_AI_API_KEY set.

Keep API keys in your secret store, out of prompts and version control. A run uses the workspace allowance and performs real actions on the site or app it is pointed at, so use it on apps and accounts you are allowed to test. These integration files are MIT licensed.
