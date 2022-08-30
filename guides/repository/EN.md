# Setting up a repository

1. Create [main branches](../../rules/repository/EN.md) - `main` и `develop`.

2. If your GitHub or GitLab plan allows you to protect branches, both `main` and `develop` need to be protected. You can enable protection in the repository settings:

**GitHub:** `Settings` -> `Branches` -> `Branch protection rules`

**GitLab:** `Settings` -> `Repository` -> `Protected branches`

Here you should also enable a requirement of an approved review from at least one team member so that Pull Request can be pushed only after approval.

> _What's the point?_ We protect critical branches from careless commits (for example, inadvertently), as well as from accidental PR merges.

3. Set the `develop` branch as default:

**GitHub:** `Settings` -> `Branches` -> `Default branch`

**GitLab:** `Settings` -> `Repository` -> `Default branch`

> _What's the point?_ This way we can be sure that the developer hasn't inadvertently branched off from `main`.

4. Allow CI:

**GitHub:** `Settings` -> `Actions` -> `Actions permissions`

**GitLab:** `Settings` -> `CI/CD` -> `General pipelines`

> _What's the point?_ In the [next section](../project/EN.md) we will configure the tests to run automatically when a new PR is opened.

1. Add a detailed README according to the [rules](../../rules/readme/EN.md).
