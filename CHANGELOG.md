## v1.0.1 (2024-01-27)

### Bug Fixes

- [#70](https://github.com/wata727/elastic_whenever/pull/70): Fix week converion issue in cron syntax

## v1.0.0 (2024-01-07)

Although this is a major version release, there are no notable incompatibilities. This means that the current behavior is stable enough that no major future changes are planned at this time.

### Enhancements

- [#69](https://github.com/wata727/elastic_whenever/pull/69): Improve profile support ([@mfittko](https://github.com/mfittko))
  - Previously, a profile passed with the `--profile` flag was always used only for shared credentials, and could not be used to switch profiles for credentials issued by IAM Identity Center, etc.
  - With this change, the passed profile will be used correctly to other credentials as well.

### Chores

- [#60](https://github.com/wata727/elastic_whenever/pull/60) [#64](https://github.com/wata727/elastic_whenever/pull/64) [#68](https://github.com/wata727/elastic_whenever/pull/68): CI against Ruby 3.1, 3.2, 3.3
- [#62](https://github.com/wata727/elastic_whenever/pull/62): fix small typo ([@kijimaD](https://github.com/kijimaD))
- [#65](https://github.com/wata727/elastic_whenever/pull/65): fix/typos-documentation ([@jotolo](https://github.com/jotolo))

## v0.7.0 (2021-09-25)

This release contains a major change to the behavior when updating tasks. In most cases, this change has no effect, but be aware of the change in behavior when omitting a revision of the task definition. In particular, if you are building a deployment workflow where the update timing of task definitions and the update timing of scheduled tasks are different, the revisions that are executed may be different.

### Breaking Changes

- [#57](https://github.com/wata727/elastic_whenever/pull/57): Selective Updates ([@HistoireDeBabar](https://github.com/HistoireDeBabar))
  - Previously, Elastic Whenever recreates all scheduled tasks after deleting all tasks when updating tasks. However, in this case, there is a risk that frequently invoked tasks will not be executed, so this change now creates/deletes only those tasks that have changed.
  - Due to this change, the naming convention for scheduled tasks has changed. When updating from v0.6, all rules will be deleted and recreated due to different naming conventions, and the behavior will be the same as before. After that, the task will not change if the names are the same.
  - The breaking change is that the behavior when omitting a revision of a task definition has changed. Previously, when you created a task, you resolved the latest revision at that time, so even if the task definition was updated, the revision that was executed was always the same. In v0.7 and later, revisions are not resolved when you created a task, so the latest revision is always adopted.

### Chores

- [#55](https://github.com/wata727/elastic_whenever/pull/55): CI against Ruby 3.0
- [#56](https://github.com/wata727/elastic_whenever/pull/56): Add the rexml dependency explictly
- [#58](https://github.com/wata727/elastic_whenever/pull/58): Fix typo

## v0.6.1 (2020-11-08)

### BugFixes

- [#51](https://github.com/wata727/elastic_whenever/pull/51): Avoid hitting rate limits fetching credentials when running under ECS or with an IAM profile  ([@stevenwilliamson](https://github.com/stevenwilliamson))

### Chores

- [#53](https://github.com/wata727/elastic_whenever/pull/53): Migrate CI to GitHub Actions from Travis CI

## v0.6.0 (2019-10-16)

### Enhancements

- [#46](https://github.com/wata727/elastic_whenever/pull/46): Add option to disable rule ([@tobscher](https://github.com/tobscher))

## v0.5.1 (2019-10-09)

### Enhancements

- [#45](https://github.com/wata727/elastic_whenever/pull/45): Add description to CloudWatch rule ([@tobscher](https://github.com/tobscher))

## v0.5.0 (2019-09-19)

### Enhancements

- [#44](https://github.com/wata727/elastic_whenever/pull/44): Make CloudWatch Events IAM role name configurable ([@domcleal](https://github.com/domcleal))

## v0.4.2 (2019-09-17)

### BugFixes

- [#43](https://github.com/wata727/elastic_whenever/pull/43): Add expression to task rule name hash computation ([@korbin](https://github.com/korbin))

### Chore

- [#42](https://github.com/wata727/elastic_whenever/pull/42): Fix typo in clear task log line ([@HistoireDeBabar](https://github.com/HistoireDeBabar))

## v0.4.1 (2019-07-23)

### BugFixes

- Retry for concurrent modification ([#41](https://github.com/wata727/elastic_whenever/pull/41))

### Chore

- CI against Ruby 2.6 ([#40](https://github.com/wata727/elastic_whenever/pull/40))

## v0.4.0 (2018-12-19)

Elastic Whenever now supports Fargate launch type. Thanks @avinson.

From this release, ECS parameters must be passed as arguments. Previously, it supported schedule file variables, but it will be ignored.

```
# Before
$ elastic_whenever --set 'cluster=ecs-test&task_definition=oneoff-application:2&container=oneoff'

# After
$ elastic_whenever --cluster ecs-test --task-definition oneoff-application:2 --container oneoff
```

### Enhancements

- update elastic_whenever for FARGATE launch type ([#34](https://github.com/wata727/elastic_whenever/pull/34))

### Changes

- Bump aws-sdk-cloudwatchevents dependency ([#36](https://github.com/wata727/elastic_whenever/pull/36))
- Pass ECS params as an argument ([#37](https://github.com/wata727/elastic_whenever/pull/37))

### Chore

- CI against Ruby 2.4.5 and 2.5.3 ([#35](https://github.com/wata727/elastic_whenever/pull/35))
- Set nil as verbose mode ([#38](https://github.com/wata727/elastic_whenever/pull/38))
- Revise task's target ([#39](https://github.com/wata727/elastic_whenever/pull/39))

## v0.3.2 (2018-06-25)

### BugFix

- fix: `Task::Role#exists?` always return true ([#33](https://github.com/wata727/elastic_whenever/pull/33))

## v0.3.1 (2018-06-25)

### BugFix

- add `attr_reader :enviroment` ([#32](https://github.com/wata727/elastic_whenever/pull/32))

### Others

- CI against Ruby 2.5 ([#30](https://github.com/wata727/elastic_whenever/pull/30))
- Use `File.exist?` instead of `File.exists?` ([#31](https://github.com/wata727/elastic_whenever/pull/31))

