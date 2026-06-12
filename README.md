# Pabot (Parallel Robot Framework) with BrowserStack

![BrowserStack Logo](https://d98b8t1nnulk5.cloudfront.net/production/images/layout/logo-header.png?1469004780)

Run your Robot Framework + SeleniumLibrary suites in parallel on the BrowserStack
device cloud using [Pabot](https://github.com/mkorpela/pabot) and the BrowserStack
Python SDK.

## Prerequisites

```
python3 should be installed
```

## Setup

* Clone the repo
  ```
  git clone -b sdk https://github.com/browserstack/pabot-browserstack.git
  cd pabot-browserstack
  ```
* It is recommended to use a virtual environment to install dependencies. To create a virtual environment:
  ```
  python3 -m venv env
  source env/bin/activate   # on Mac/Linux
  env\Scripts\activate      # on Windows
  ```
* Install dependencies
  ```
  pip install -r requirements.txt
  ```
* Set your BrowserStack credentials. Add your `userName` and `accessKey` in the
  `browserstack.yml` config file, or export them as environment variables:

  #### For Linux/MacOS
  ```
  export BROWSERSTACK_USERNAME=<browserstack-username>
  export BROWSERSTACK_ACCESS_KEY=<browserstack-access-key>
  ```
  #### For Windows
  ```
  set BROWSERSTACK_USERNAME=<browserstack-username>
  set BROWSERSTACK_ACCESS_KEY=<browserstack-access-key>
  ```

## Run Sample Test

Run the sample suite in parallel across the platforms defined in `browserstack.yml`:

```
browserstack-sdk pabot --processes 2 --testlevelsplit tests/sample-test.robot
```

To run every suite under `tests/` in parallel:

```
browserstack-sdk pabot --processes 2 --testlevelsplit tests/
```

## Run Local Test

Start the local web server hosting `tests/local-test.robot`'s target (the SDK starts
the BrowserStack Local tunnel automatically because `browserstackLocal: true` is set in
`browserstack.yml`), then run:

```
browserstack-sdk pabot --processes 2 --testlevelsplit tests/local-test.robot
```

## Notes

* View your test runs, sessions, logs, and Test Observability reports on the
  [BrowserStack Automate dashboard](https://automate.browserstack.com/).
* `pabot` is the parallel runner for Robot Framework; `--processes` controls how many
  worker processes run concurrently and `--testlevelsplit` splits at the test-case level
  so each test can land on its own parallel session.
* Understand how many parallel sessions you need with the
  [Parallel Test Calculator](https://www.browserstack.com/automate/parallel-calculator?ref=github).
