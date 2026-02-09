## Basics
it's an automation CI/CD tools used to deploy/perform certain tasks when certain events take place

```yml
# example
# in repo - .github/workflows/main.yml
name: hello # enter name
'on': push, pull, ...
    branches: ["main"]
jobs:
    name:
        runs-on: ubuntu-latest
        steps:
            - name: my-steps
            run: echo "Hello World"
```

`(name)` workflow &rarr; collection of jobs

`(on)` events &rarr; any activity that is triggered

`(jobs)` jobs &rarr; collection of steps (can chain jobs)

`(steps)` steps &rarr; actions to be taken