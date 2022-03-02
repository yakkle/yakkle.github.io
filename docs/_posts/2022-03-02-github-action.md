# GitHub action?
## CI/CD
 - Continuous Integration and Continuous Delivery
 - automate your build, test and deployment

## Components
 ![image](https://user-images.githubusercontent.com/4245169/147060738-40385522-d469-427d-82b5-2606c25ea057.png)
 - workflow
 - [events][Components events]
   - push, pull_request, schedule, workflow_dispatch...
 - jobs
   - build, deploy...
 - actions
   - [checkout][Actions checkout], [setup-python][Actions setup-python]...
 - [runners][Components runners]
   - ubuntu linux, MS windows, macos

# [Quick start](https://docs.github.com/en/actions/quickstart)

## first example
 - .github/workflows 에 `first.yml` 을 만들고 아래 내용을 붙여 넣는다.

```yml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

# Build and Test(CI)

## python example
[build and test python][build test python]

```yml
name: Python package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.6, 3.7, 3.8, 3.9]

    steps:
      - uses: actions/checkout@v2
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install flake8 pytest
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
      - name: Lint with flake8
        run: |
          # stop the build if there are Python syntax errors or undefined names
          flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
          # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
          flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
      - name: Test with pytest
        run: |
          pytest
```

 - events
 - jobs
   - runs-on
   - strategy
   - steps

# deployment(CD)

## [deploy to amazon][deploy to amazon ECS]
 - workflow example
```yml
```

## [deploy to azure][deploy to azure]
 - workflow example
```yml
```


# Practical example
 - [icon-sdk-python](https://github.com/icon-project/icon-sdk-python)
 - [icon-tracker-frontend](https://github.com/icon-project/icon_tracker_frontend)

# Learn more
 - [Expressions][More expressions]
 - [Contexts][More contexts]
 - [Workflow syntax][More workflow syntax]

# Etc.
 - [run locally](https://github.com/nektos/act)
 - [awesome actions](https://github.com/sdras/awesome-actions)

---- 
self learning github action : [learning lab][GitHub Actions: Hello World]


<!-- Links -->
[Components events]: https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows
[Components runners]: https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources
[Actions checkout]: https://github.com/actions/checkout
[Actions setup-python]: https://github.com/actions/setup-python

[build test python]: https://docs.github.com/actions/automating-builds-and-tests/building-and-testing-nodejs-or-python?langId=py
[deploy to amazon ECS]: https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-amazon-elastic-container-service
[deploy to azure]: https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure
[GitHub Actions: Hello World]: https://lab.github.com/githubtraining/github-actions:-hello-world

[More expressions]: https://docs.github.com/en/actions/learn-github-actions/expressions
[More contexts]: https://docs.github.com/en/actions/learn-github-actions/contexts
[More workflow syntax]: https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions