# tunnelliers/.github — profil public de l'org et workflows partagés

Team rules: injected by the `tunnelliers` plugin at session start (`studio/plugins/tunnelliers/team-rules.md`).

- **PUBLIC repo**: everything here is visible to the world. Never put secrets, ids of private experiences, internal
  links or unreleased game details here.
- `profile/README.md` = the org's public page. `.github/workflows/luau-ci.yml` = reusable Luau CI (Rokit authenticated
  with the workflow token, Rojo build, typecheck); keep it in sync with `games/.github/workflows/ci.yml` when the
  install or build steps change there. Issue / PR templates also live here.
