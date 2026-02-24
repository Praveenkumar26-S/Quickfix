### quickfix

quickfix

### Installation

You can install this app using the [bench](https://github.com/frappe/bench) CLI:

```bash
cd $PATH_TO_YOUR_BENCH
bench get-app $URL_OF_THIS_REPO --branch version-16
bench install-app quickfix
```

### Contributing

This app uses `pre-commit` for code formatting and linting. Please [install pre-commit](https://pre-commit.com/#installation) and enable it for this repository:

```bash
cd apps/quickfix
pre-commit install
```

Pre-commit is configured to use the following tools for checking and formatting your code:

- ruff
- eslint
- prettier
- pyupgrade
### CI

This app can use GitHub Actions for CI. The following workflows are configured:

- CI: Installs this app and runs unit tests on every push to `develop` branch.
- Linters: Runs [Frappe Semgrep Rules](https://github.com/frappe/semgrep-rules) and [pip-audit](https://pypi.org/project/pip-audit/) on every pull request.


### License

mit

### Answers
A2 - Multi-Site & Configuration

1. what each config file is for, and what breaks if you accidentally put a secret in common_site_config.json?

The site_config is stores the specific configuration of the site like db credentials, but in the common_site_config it stores the all sites configuration in the bench like shared db, redis. If the secret is been in the common_site_config it leads to the security issues and to data leakages also.

2. list the 4 processes bench start launches (web, worker, scheduler,socketio) and explain what happens to background jobs if the worker process crashes.

If we start the bench the profile has been initialized in that  the six process has been started, web is for to connect the HTTP request and the application to the user through the browser, second one is worker this executes the background jobs in the redis queue, third one scheduler this queue the scheduler job to the redis queue and the last one is socketio this enables the realtime process and features to notify the client. If the worker process is been crashes in the background jobs, the background jobs are been stop executing and again set to the queue after the worker got been restarted the jobs is been executing, the remainin two process are one is web this starts the frappe web server, and the watch is used to rebuild the backend code in the frontend without rebuild the bench in the developement mode only.