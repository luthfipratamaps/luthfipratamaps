# Accurate GitHub Profile Stats Setup

This pack replaces the three external stats images in the README with SVG cards
generated inside your own GitHub profile repository.

## Files

Place these in `luthfipratamaps/luthfipratamaps`:

- `README.md`
- `.github/workflows/update-profile-stats.yml`

The workflow will generate:

- `profile-summary-card-output/github_dark/0-profile-details.svg`
- `profile-summary-card-output/github_dark/2-most-commit-language.svg`
- `profile-summary-card-output/github_dark/3-stats.svg`

The README already points to those generated files.

## 1. Enable private contribution visibility

On GitHub:

Settings -> Public profile -> Contribution settings

Enable:

`Include private contributions on my profile`

This exposes contribution COUNTS only. It does not expose private repository
names, commit messages, issue titles, or other private repository contents in
the generated cards.

## 2. Create a token for accurate private-repository stats

The action needs a token that can read the repositories you want counted.

For a classic Personal Access Token, the action documentation recommends:

- `repo`
- `read:user`

If organization repositories use SSO or organization approval, make sure the
token is authorized for that organization as required by its policy.

## 3. Save the token as a repository secret

Open:

`luthfipratamaps/luthfipratamaps`
-> Settings
-> Secrets and variables
-> Actions
-> New repository secret

Name:

`SUMMARY_GITHUB_TOKEN`

Paste the token as the value.

Never place the raw token in README.md or the workflow YAML.

## 4. Commit the files

Your repository should look like:

```text
luthfipratamaps/
├── README.md
└── .github/
    └── workflows/
        └── update-profile-stats.yml
```

## 5. Run once manually

GitHub repository -> Actions -> Update GitHub Profile Summary Cards
-> Run workflow

After it succeeds, the action creates the `profile-summary-card-output/`
folder and commits the generated SVG cards to the repository.

After that it updates automatically once per day.

## Notes on accuracy

With a token that can access your private repositories AND GitHub's
"Include private contributions on my profile" setting enabled:

- Total commits can include private-repository activity.
- Total pull requests can include private-repository activity.
- Total issues can include private-repository activity.
- The profile-details contribution graph can include private contributions.
- Language cards can include accessible private repositories.

Some metrics such as total stars remain public-only by design in the summary
cards project, so they should not be interpreted as a complete private-work
metric.
