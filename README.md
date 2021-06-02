## how to test config.yml
ref: https://circleci.com/docs/2.0/local-cli/

Regarding Orbs, see https://github.com/vsanna/dd_orb

```bash
brew install circleci
circleci setup

circleci config validate
circleci orb validate path/to/myorb.yml

circleci local execute --job {jobname}

# namespace create command should be run only once
circleci namespace create vsanna github vsanna

# setup orbs project
circleci orb init
# if you already have orb projects, you can use create instead of init
circleci orb create
circleci orb publish src/@orb.yml vsanna/dd_orb@dev:alpha
circleci orb publich development version
circleci orb publich production version
```

## orb development flow
- change
- validate
- merge
    - master mergeで勝手に出してくれるっぽい. tagは?
    - commit msgに `[semver:major] first orb release.` これ必要


## orb dir structure
Orb contains commands, jobs and executors. (these three sections are reusable)

SEE:
- https://circleci.com/docs/2.0/orb-author-intro/
- https://circleci.com/docs/2.0/orb-author/

```bash
.
├── CHANGELOG.md
├── LICENSE
├── README.md
└── src
    ├── @orb.yml
    ├── README.md
    ├── commands       # 1 command per 1 file
    │   ├── README.md
    │   └── greet.yml
    ├── executors      # 1 executor per 1 file
    │   ├── README.md
    │   └── default.yml
    ├── jobs
    │   ├── README.md
    │   └── hello.yml
    ├── scripts
    │   ├── README.md
    │   └── greet.sh
    └── tests
        ├── README.md
        └── greet.bats

```

https://circleci.com/docs/2.0/creating-orbs/#issue-a-new-release

From alpha branch, open a PR with title like `[semver:major] first orb release.`