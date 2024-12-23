# wasmCloud Org Admin

This repository contains the [clowarden.yaml](./clowarden.yaml) manifest that is interpreted by [CLOWarden](https://github.com/cncf/clowarden) to manage access to resources in the wasmCloud organization. It reconciles the contents of the clowarden file and the current state of the wasmCloud organization, making sure that it's up-to-date and reflects desired state. Primarily this file is modified to add new maintainers to existing teams, modify members of existing teams, and add new repositories to the wasmCloud organization.

## Modifying maintainers of a team

Find the existing team in [clowarden.yaml](./clowarden.yaml) and add or remove the new maintainer (by GitHub handle) to the desired team (by GitHub team slug) under the **members** section. Add the maintainer in alphabetical order to keep the list nice and ordered. Create a pull request denoting which maintainer is being added and request a review from the team in question.

## Adding a new repository

At the bottom of the [clowarden.yaml](./clowarden.yaml), create a new repository by adding the following template in alphabetical repository order:

```yaml
- name: <repository-name>
  teams:
    <primary-maintainer-team>: maintain
    org-maintainers: admin
  visibility: public
```

For example, if I wanted to add a new GitHub action repository for re-use across the organization, I would add:

```yaml
  - name: setup-wash
    teams:
      ci-maintainers: maintain
      org-maintainers: admin
    visibility: public
```

wasmCloud `org-maintainers` should always have `admin` access on a repository to faciliate metadata updates, branch protection rules, and general management. You can add multiple teams to the list if applicable. Refer to the [CLOWarden Configuration](https://github.com/cncf/clowarden#configuration) documentation for additional options.
