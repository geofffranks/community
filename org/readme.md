# Management of github organization cloudfoundry

The projects, teams and org membership in github org 'cloudfoundry' are maintained according to a number of [RFCs](https://github.com/cloudfoundry/community/tree/main/toc/rfc). The RFCs require PRs to one of the following files:

- [cloudfoundry.yml](https://github.com/cloudfoundry/community/blob/main/org/cloudfoundry.yml) - static org configuration and projects
- [contributors.yml](https://github.com/cloudfoundry/community/blob/main/org/contributors.yml) - list of [Contributors](https://github.com/cloudfoundry/community/blob/main/toc/ROLES.md#contributor)
- [TOC.md](https://github.com/cloudfoundry/community/blob/main/toc/TOC.md) - projects owned by the TOC (specified in yaml block)
- [Working Group Charters](https://github.com/cloudfoundry/community/tree/main/toc/working-groups) - projects owned by working groups (specified in yaml block)

Once approved and merged, the github action [org-management.yml](https://github.com/cloudfoundry/community/actions/workflows/org-management.yml) compiles a resulting cloudfoundry org configuration from the files mentioned above and applies it with [peribolos](https://github.com/kubernetes/test-infra/tree/master/prow/cmd/peribolos).

[org_management.py](https://github.com/cloudfoundry/community/blob/main/org/org-management.py) generates the following parts of the resulting cloudfoundry org configuration:

### Organization Members 
Organization members are generated according to [rfc-0002-github-members](https://github.com/cloudfoundry/community/blob/main/toc/rfc/rfc-0002-github-members.md) and [rfc-draft-role-change-process](https://github.com/cloudfoundry/community/pull/248):
- any members specified in [cloudfoundry.yml](https://github.com/cloudfoundry/community/blob/main/org/cloudfoundry.yml) (should be none)
- all contributors from [contributors.yml](https://github.com/cloudfoundry/community/blob/main/org/contributors.yml)
- all working group leads and approvers specified in the [Working Group Charters](https://github.com/cloudfoundry/community/tree/main/toc/working-groups)
- org admins and TOC members must not be added to org member list

### Organization Admins
TODO: add TOC members specified in [TOC.md](https://github.com/cloudfoundry/community/blob/main/toc/TOC.md) as org admins 

### Github Teams for Working Group Areas
TODO: generation of github teams according to [rfc-0005-github-teams-and-access](https://github.com/cloudfoundry/community/blob/main/toc/rfc/rfc-0005-github-teams-and-access.md)

## Development

Requires Python 3.9.

How to run locally:
```
pip install -r requirements.txt
python -m org_management --help
```

Usage:
```
$ python -m org_management --help
usage: org_management.py [-h] [-o OUT]

Cloud Foundry Org Generator

optional arguments:
  -h, --help         show this help message and exit
  -o OUT, --out OUT  output file for generated org configuration
```

How to run tests:
```
pip install -r requirements-dev.txt
python -m flake8
python -m unittest discover -s .
```