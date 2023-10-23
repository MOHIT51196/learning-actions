# Github Actions

- one repo can have multiple workflows
- workflow > job > step > action
- path is .github/workflows

## General syntax
```
name: <workflow name> # optional
on: [ <trigger> ]
jobs:
  <job name>:
    runs-on: <os environment>
    steps:
      - name: <step name> # optional
        run: <command>
        # OR
        uses: <in-built/custom actions>
```

## Triggers
- events
  - pull request
  - push
  - release
- webhooks
  - branch event
  - member event
  - issues
- schedule : cron jobs

### Syntax
```
on:
  push:
    branches:
      - master
      - feature/*
  pull_request:
    branches:
      - master  
```

- `branches-ignore` can also be used to ignore branches
- `tags` or `tags-ignore` can be used just as branches

## Jobs
- Atleast one job is required in workflow
- Job name should start with a letter or underscore (no special characters are recommended)
- Jobs should complete in **6 hours** runtime

### Concurrency
| Plan | Concurrent jobs |
| ---- | ---- |
| Free | 20 |
| Pro | 40 |
| Team | 60 |
| Enterprise | 180 ( `Barco` ) |

## Runners
- Type of runners
  - Windows server 2019
  - Ubuntu 16, 18
  - macOS Catalina
  - Self hosted

- `run` is used to run shell command in virtaul env
- Default shell for linux, macOS is `bash` and for windows is `powershell`

## Limits & Quota
- Actions can't trigger other workflows
- Action logs are limited to 64kb
- 1000 API request/hour to github from workflows
- Job can take max 6 hours of runtime

*NOTE : Exceeding these limits result in job queuing or even failing*

## Dependencies

Usecase : if job 1 and job2 needs to run before job 3 as dependencies so that input from job 1 and 2 can go to job 3. Use `needs` property

```
name: <workflow name>
on: <trigger>
jobs:
  job1:
    ...
  job2:
    ...
  job3:
    needs: [job1, job2]  # job 1 and 2 can run parallel but will run before job 3 always
```
