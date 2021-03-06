# Minishift Boot2Docker ISO
This repository contains all required instructions and code to build an ISO based on [Boot2Docker](https://github.com/boot2docker/boot2docker) to use with [minishift](https://github.com/minishift/minishift).

----

<!-- MarkdownTOC -->

- [Building the minishift-b2d ISO](#building-the-b2d-iso)
    - [Prerequisites](#prerequisites)
    - [Building the ISO](#building-the-iso)
    - [Using the ISO](#using-the-iso)
- [Tests](#tests)
- [Releasing the minishift-b2d ISO](#releasing-the-b2d-iso)
    - [Prerequisites](#release-prerequisites)
    - [Releasing the ISO](#releasing-the-iso)
- [CI Setup](#ci-setup)
- [History](#history)
- [Community](#community)

<!-- /MarkdownTOC -->

[![Build Status](https://ci.centos.org/buildStatus/icon?job=minishift-b2d-iso)](https://ci.centos.org/job/minishift-b2d-iso/)

----

<a name="building-the-b2d-iso"></a>
## Building the minishift-b2d ISO

The minishift-b2d.iso is built via a Dockerfile.

<a name="prerequisites"></a>
### Prerequisites

* A running docker daemon.

<a name="building-the-iso"></a>
### Building the ISO

```
$ git clone https://github.com/minishift/minishift-b2d-iso.git
$ cd minishift-b2d-iso
$ make
```
- The ISO should be present in `minishift-b2d-iso/build` directory after the successful run of `make`.

<a name="using-the-iso"></a>
### Using the ISO
- The ISO can be used with [minishift](https://github.com/minishift/minishift) with the help of `--iso-url` i.e. `--iso-url=file:///$PATHTOISO`.

<a name="tests"></a>
## Tests

Tests are written as Python scripts under `tests` directory and run through [Avocado](avocado-framework.readthedocs.io) framework. Ensure you have _Avocado_ installed by following [Avocado instllation guide](http://avocado-framework.readthedocs.io/en/44.0/GetStartedGuide.html#installing-avocado) before running any tests.

Build ISO:
```
$ make
```

Run the tests:
```
$ make test
```

If you want to see the logs generated by test, run the test as:
```
$ SHOW_LOG=--show-job-log make test
```

<a name="releasing-the-b2d-iso"></a>
## Releasing the minishift-b2d ISO

<a name="release-prerequisites"></a>
### Prerequisites

- Working installation of [Go](https://en.wikipedia.org/wiki/Go_(programming_language)) with `GOPATH` properly set.
- A running docker daemon.

<a name="releasing-the-iso"></a>
### Releasing the ISO

- Assemble all the meaningful changes since the last release to create release notes.
- Bump the `VERSION` variable in the Makefile.
- Make sure to have a [Github personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use) defined in your environment as `GITHUB_ACCESS_TOKEN`.
- Run following command to release the ISO:

```
$ make release
```

<a name="ci-setup"></a>
## CI Setup

`minishift-b2d-iso` uses [CentOS CI](https://ci.centos.org/) as CI build server.
It builds incoming pull requests and any push to master along with archiving the build artifacts.
You can find the CentOS CI jenkins master job [here](https://ci.centos.org/job/minishift-b2d-iso/) and the pull request job [here](https://ci.centos.org/job/minishift-b2d-iso-pr/).

On a successful pull request build, the build artifacts can be found at
[artifacts.ci.centos.org/minishift/minishift-b2d-iso/pr/\<PR ID\>](http://artifacts.ci.centos.org/minishift/minishift-b2d-iso/pr/).

On a successful master build, the build artifacts can be found at
[artifacts.ci.centos.org/minishift/minishift-b2d-iso/master/\<BUILD ID\>](http://artifacts.ci.centos.org/minishift/minishift-b2d-iso/master/).

For more information about CentOS CI, check out its [Wiki](https://wiki.centos.org/QaWiki/CI) to
know more about CentOS CI.

<a name="history"></a>
## History

- This repository is created by exracting the `iso` directory of [Minishift](https://github.com/minishift/minishift) project.

<a name="community"></a>
## Community

You can reach the Minishift community by:

- Signing up to our [mailing list](https://lists.minishift.io/admin/lists/minishift.lists.minishift.io)

- Joining the `#minishift` channel on [Freenode IRC](https://freenode.net/)
