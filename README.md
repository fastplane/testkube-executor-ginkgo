![Testkube Logo](https://raw.githubusercontent.com/kubeshop/testkube/main/assets/testkube-color-gray.png)
                                                           
# Welcome to the Testkube Ginkgo Executor

The Kubetest Ginkgo Executor is a test executor for [testkube](https://testkube.io).

# Issues and enchancements 

Please visit the main Testkube repository for reporting any [issues](https://github.com/kubeshop/testkube/issues) or [discussions](https://github.com/kubeshop/testkube/discussions).

## Details 

### Supports Git Repo Testing Only
**Example `kubectl testkube create test` call, git by branch:**

`$ kubectl testkube create test --git-uri <URI TO A GOLANG REPO THAT CONTAINS GINKGO TESTS> --git-branch main --name ginkgo-test --type ginkgo/test --git-username <GIT USER> --git-token=<GIT TOKEN>`

**Example `kubectl testkube create test` call, git by commit id:**

`$ kubectl testkube create test --git-uri <URI TO A GOLANG REPO THAT CONTAINS GINKGO TESTS> --git-commit <GIT COMMIT ID/SHA> --name ginkgo-test --type ginkgo/test --git-username <GIT USER> --git-token=<GIT TOKEN>`

### Parameters:
Pass in/override Ginkgo parameters with -v Variables. 
* `GinkgoTestPackage`, default: `""`
* `GinkgoRecursive`, default: `-r`
* `GinkgoParallel`, default: `-p`
* `GinkgoParallelProcs`, default: `""`, usage: `--procs N`
* `GinkgoCompilers`, default: `""`, usage: `--compilers N`
* `GinkgoRandomize`, default: `--randomize-all`
* `GinkgoRandomizeSuites`, default: `--randomize-suites`
* `GinkgoLabelFilter`, default: `""`, usage: `--label-filter QUERY`
* `GinkgoFocusFilter`, default: `""`, usage: `--focus REGEXP`
* `GinkgoSkipFilter`, default: `""`, usage: `--skip REGEXP`
* `GinkgoUntilItFails`, default: `""`, usage: `--until-it-fails`
* `GinkgoRepeat`, default: `""`, usage: `--repeat N`
* `GinkgoFlakeAttempts`, default: `""`, usage: `--flake-attempts N`
* `GinkgoTimeout`, default: `""`, usage: `--timeout=duration`
* `GinkgoSkipPackage`, default: `""`, usage: `--skip-package list,of,packages`
* `GinkgoFailFast`, default: `""`, usage: `--fail-fast`
* `GinkgoKeepGoing`, default: `""`, usage: `--keep-going`
* `GinkgoFailOnPending`, default: `""`, usage: `--fail-on-pending`
* `GinkgoCover`, default: `""`, usage: `--cover`
* `GinkgoCoverProfile`, default: `""`, usage: `--coverprofile cover.profile`
* `GinkgoRace`, default: `""`, usage: `--race`
* `GinkgoTrace`, default: `"--trace"`
* `GinkgoJsonReport`, default: `""`, usage: `--json-report report.json`
* `GinkgoJunitReport`, default: `"--junit-report report.xml"`
* `GinkgoTeamCityReport`, default: `""`, usage: `--teamcity-report report.teamcity`

### Pass-through args to Ginkgo:
Add `--args '--base-url=example.com --some-arg=value'` to `kubectl testkube run test` command.

### Example CLI Test Execution Calls
* `kubectl testkube run test ginkgo-test -f` : Executes the testkube named `ginkgo-test` and will run (recursively, with -r flag) all Ginkgo tests within the repo.
* `kubectl testkube run test ginkgo-test -f -v GinkgoTestPackage=e2e` : Executes the testkube named `ginkgo-test` and overrides `GinkgoTestPackage` to run the `e2e` package in the repo.
* `kubectl testkube run test ginkgo-test -f -v GinkgoSkipPackage="--skip-package other,other2" -v GinkgoParallel=""` : Executes the testkube and skips packages named `other` and `other2`, as well as turns _off_ Parallel Execution.
* `kubectl testkube run test ginkgo-test -f -v GinkgoTestPackage=e2e ---args '--base-url=example.com'` : Executes the e2e test package and provies a passthrough arg named `base-url` set to `example.com`.

## Architecture

- TODO add architecture diagrams

## API 

Cypress executor implements [testkube OpenAPI for executors](https://kubeshop.github.io/testkube/openapi/#operations-tag-executor) (look at executor tag).
