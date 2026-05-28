## Stack
JavaScript (9% of codebase), Docker. No framework detected; likely a lightweight UI service for flagd feature flags.

## Constraints
Never modify:
- `package-lock.json`, `yarn.lock`, or any lock files
- `*.env`, `.env*`, credential or secret files
- Any generated or compiled output directories (`dist/`, `build/`, `.next/`)
- Dockerfile `FROM` digest pins once hardened (lines containing `@sha256:`)
- Test fixture files or snapshot files

## Conventions
- Tests live alongside source files or in a `test/` or `__tests__/` directory; test files are named `*.test.js` or `*.spec.js`
- Docker images are defined in `Dockerfile` at repo root or subdirectories
- Dead code removal targets only `.js` files; do not remove exports that may be consumed externally without a local import

## Dependency manifests
- `package.json` — primary Node.js dependency and script declarations
- `package-lock.json` — locked dependency tree (read-only; regenerate via `npm install` after editing `package.json`)

## Notes for maintenance agents
- `dependency_updates`: edit only `package.json` version ranges; run `npm install` to regenerate lock file; do not bump major versions without a passing test suite
- `docker_hardening`: pin base images to `image@sha256:` digests; add `USER nonroot`, drop capabilities, set `--no-cache` on `apk`/`apt` install steps
- `dead_code_removal`: only remove code with no reachable references within the repo; when in doubt, leave it
- `cve_scan` / `security`: if 0 files changed is reported repeatedly, verify tooling version is current before assuming clean
