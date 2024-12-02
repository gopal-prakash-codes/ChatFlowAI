
### Managing environments


pyenv install 3.10.10
pyenv local 3.10.10  # Activate Python 3.10.10 for the current project
```
*Note*: If you have trouble installing a specific version of python on your system
it might be worth trying other supported versions.

By default, Poetry will try to use the currently activated Python version to create the virtual environment
for the current project automatically. You can also create and activate a virtual environment manually — in this
case, Poetry should pick it up and use it to install the dependencies. For example:

```bash
python -m venv .venv
source .venv/bin/activate
```

You can make sure that the environment is picked up by executing

```bash
poetry env info
```

### Building from source

To install dependencies and `rasa` itself in editable mode execute

```bash
make install
```

*Note for macOS users*: under macOS Big Sur we've seen some compiler issues for
dependencies. Using `export SYSTEM_VERSION_COMPAT=1` before the installation helped.


#### Installing optional dependencies

In order to install rasa's optional dependencies, you need to run:

```bash
make install-full
```


In order to resolve it, you must follow these steps to install a Rust compiler:
```bash
brew install rustup
rustup-init
```

After initialising the Rust compiler, you should restart the console and check its installation:
```bash
rustc --version
```

In case the PATH variable had not been automatically setup, run:
```bash
export PATH="$HOME/.cargo/bin:$PATH"
```


### Running and changing the documentation

First of all, install all the required dependencies:

```bash
make install install-docs
```

After the installation has finished, you can run and view the documentation
locally using:

```bash
make livedocs
```

It should open a new tab with the local version of the docs in your browser;
if not, visit http://localhost:3000 in your browser.
You can now change the docs locally and the web page will automatically reload
and apply your changes.

### Running the Tests

In order to run the tests, make sure that you have the development requirements installed:

```bash
make prepare-tests-ubuntu # Only on Ubuntu and Debian based systems
make prepare-tests-macos  # Only on macOS
```

Then, run the tests:

```bash
make test
```

They can also be run at multiple jobs to save some time:

```bash
JOBS=[n] make test
```

Where `[n]` is the number of jobs desired. If omitted, `[n]` will be automatically chosen by pytest.


### Running the Integration Tests

In order to run the integration tests, make sure that you have the development requirements installed:

```bash
make prepare-tests-ubuntu # Only on Ubuntu and Debian based systems
make prepare-tests-macos  # Only on macOS
```

make run-integration-containers
```

Finally, you can run the integration tests like this:

```bash
make test-integration
```



```bash
pip install poetry-merge-lock
```

Just execute this command to resolve merge conflicts in `poetry.lock` automatically:

```bash
poetry-merge-lock
```

### Build a Docker image locally

In order to build a Docker image on your local machine execute the following command:

```bash
make build-docker
```

The Docker image is available on your local machine as `rasa:localdev`.


#### Formatting

If you want to automatically format your code on every commit, you can use [pre-commit](https://pre-commit.com/).
Just install it via `pip install pre-commit` and execute `pre-commit install` in the root folder.
This will add a hook to the repository, which reformats files on every commit.

If you want to set it up manually, install black via `poetry install`.
To reformat files execute
```
make formatter
```

#### Type Checking

If you want to check types on the codebase, install `mypy` using `poetry install`.
To check the types execute
```
make types
```