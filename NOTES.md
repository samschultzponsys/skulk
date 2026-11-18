# Notes — open items

## Blocked on the user
- **Finish the Skulk rename (1.9).**
  - The repo is renamed to `skulk`. CI publishes to `ghcr.io/samschultzponsys/skulk-ipam`
    (set in the workflow). The first 1.9 build also went to
    `ghcr.io/samschultzponsys/skulk` before that fix; that package can be deleted.
  - After the first build, check the new `skulk-ipam` package's visibility in
    GitHub → Packages (make it public if the old one was).
  - Switch the server's compose to `skulk-ipam` (see the readme).
- **Issues panel (1.7) needs a token permission.** Edit the fine-grained token used
  for update checks and add *Issues: Read and write* on this repo. Until then the
  panel can read but posts wait as "not sent"; they go out on the next sync once
  the permission is added.
- **Backfill GitHub Releases v1.0–v1.5.**
  - Add a `RELEASE_TOKEN` repo secret. Either works:
    - a fine-grained PAT on this repo with Contents and Workflows set to read & write
    - a classic PAT with the `repo` and `workflow` scopes
  - Then run Actions → build-image → Run workflow. `publish-releases.sh` will tag
    each old version on its original commit and fill in the notes.
  - v1.6 onwards are published automatically.

## Unverified / needs real hardware
- Omada reservation field names (`ipSetting`, `fixedIp`) are a best guess.
- Every platform except UniFi has been tested only against fake controllers.
  Alta Labs Route10 (SSH) is marked experimental.
- The GitHub Issues sync (1.7) has been tested only against a fake GitHub API.
  Things to check against real GitHub:
  - that a fine-grained token with *Issues: Read and write* can post
  - that the *full* media type returns `body_html`
  - how `<sub>` signatures and private image links render
- OIDC has been tested only against a fake IdP. Try Authentik, Pocket ID or Keycloak.
- The phone layout has been checked only in Playwright's mobile viewport, not on
  real iOS or Android devices.

## Maintenance
- GitHub Actions warns that Node 20 actions are deprecated. Bump
  `actions/checkout@v4` and the `docker/*` actions when new majors are out.
