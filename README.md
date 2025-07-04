# Awesome pre-commit

A curated list of awesome [pre-commit](pre-commit.com) hooks and related resources.

The official [list of supported hooks](https://pre-commit.com/hooks.html) was previously a [great resource](https://web.archive.org/web/20231005000108/pre-commit.com/hooks) for discovering new hooks. The new suggested approach of [finding hooks](https://pre-commit.com/hooks.html#finding-hooks) works ok, but it can still be difficult to find what you're looking for, or discover new hooks you didn't know you needed. This repo seeks primarily to serve as that resource.

<!-- mdformat-toc start --slug=github --no-anchors --maxlevel=6 --minlevel=2 -->

- [Hooks](#hooks)
  - [C/C++](#cc)
  - [CMake](#cmake)
  - [Dockerfile](#dockerfile)
  - [Documentation](#documentation)
  - [Images](#images)
  - [JSON](#json)
  - [Makefile](#makefile)
  - [Markdown](#markdown)
  - [Protocol Buffers](#protocol-buffers)
  - [Python](#python)
  - [Shell](#shell)
  - [Spellchecking](#spellchecking)
  - [YAML](#yaml)
- [Additional Resources and Tips](#additional-resources-and-tips)
  - [Tool Setup](#tool-setup)
    - [`additional_dependencies`](#additional_dependencies)
    - [Dev Environments](#dev-environments)

<!-- mdformat-toc end -->

## Hooks

### C/C++

- https://github.com/pre-commit/mirrors-clang-format - Formats C, C++, Objective-C, and Java code
- https://github.com/Takishima/cmake-pre-commit-hooks - Static analysis hooks leveraging `compile_commands.json` for CMake-based projects
  - clang-tidy - Linter
  - cppcheck - Static analyzer
  - include-what-you-use - `#include` linter

### CMake

- https://github.com/cheshirekow/cmake-format-precommit
  - cmake-format - Formatter
  - cmake-lint - Linter
- https://github.com/BlankSpruce/gersemi - Formatter
- https://github.com/cmake-lint/cmake-lint - Linter

### Dockerfile

- https://github.com/AleksaC/hadolint-py - Linter

### Documentation

- https://github.com/adamchainz/blacken-docs - Formats Python code blocks within documentation
- https://github.com/amperser/proselint - Linter

### Images

- https://github.com/shssoichiro/oxipng - PNG optimizer

### JSON

- https://github.com/maresb/check-json5 - Checks JSON syntax (allows comments, trailing commas, etc.)
- https://github.com/python-jsonschema/check-jsonschema - JSON schema validation

### Makefile

- https://github.com/mrtazz/checkmake - Linter

### Markdown

- https://github.com/hukkin/mdformat - Formatter
- https://github.com/tcort/markdown-link-check - Checks for dead hyperlinks

### Protocol Buffers

- https://github.com/bufbuild/buf
  - buf-generate - Auto-generates source code from proto file
  - buf-breaking - Enforces compatibility when proto file changes
  - buf-lint - Linter
  - buf-format - Formatter
  - buf-dep-update - Updates dependencies
  - buf-dep-prune - Removes unused dependencies
- https://github.com/yoheimuta/protolint - Linter

### Python

- https://github.com/charliermarsh/ruff-pre-commit
  - ruff - Linter
  - ruff-format - Formatter
- https://github.com/psf/black
  - black - Formatter
  - black-jupyter - Formatter (for Jupyter Notebooks)

### Shell

- https://github.com/MaxWinterstein/shfmt-py - Formatter
- https://github.com/shellcheck-py/shellcheck-py - Linter
- https://github.com/openstack/bashate - Linter/style checker
- https://github.com/lovesegfault/beautysh - Formatter

### Spellchecking

- https://github.com/crate-ci/typos - Spell checker/fixer

### YAML

- https://github.com/mschuett/yaml-shellcheck
  - yaml-shellcheck - Lints shell scripts in yaml files (such as .gitlab-ci.yml)
- https://github.com/google/yamlfmt - Formatter
- https://github.com/adrienverge/yamllint - Linter

## Additional Resources and Tips

### Tool Setup

When using pre-commit on a development team, it is important for all developers to be using the same versions of the tools that their pre-commit hooks depend on. For many hooks, pre-commit will automatically bootstrap the appropriate package manager (if needed) and install the tools into a Python virtual environment for you; unfortunately other hooks rely on system-installed tools that pre-commit must assume are available. To work around this, there are several options:

#### `additional_dependencies`

When you need to use a hook whose [language](https://pre-commit.com/#supported-languages) supports the [`additional_dependencies`](https://pre-commit.com/#config-additional_dependencies) property, check if the language's package manager has an implementation of the tool, and specify it there. This is somewhat common for Python.

As an example, the hooks for the https://github.com/pocc/pre-commit-hooks repo will not install the tools automatically. But many of the tools can be installed automatically by pre-commit via pip, just by adding the appropriate values to `additional_dependencies`, such as [`clang-format`](https://pypi.org/project/clang-format/) or [`clang-tidy`](https://pypi.org/project/clang-tidy/) -- just remember to pin the package version!

#### Dev Environments

Set up a dev environment containing your desired pre-commit hook dependencies (as well as other dependencies) using one of the available options:

- [Dev Containers](https://containers.dev/)
  - Docker-based
  - Integrates into popular code editors
- [Nix](https://nix.dev/) Package Manager
- [Devbox](https://www.jetify.com/devbox/)
  - Nix-based (but more user-friendly)
  - Can be hosted in the Cloud
  - Can generate Dev Container definitions and Dockerfiles
- [Pixi](https://pixi.sh)
  - Conda-based

When using a non-Docker-based dev environment, it is highly recommended to use [direnv](https://direnv.net/) (or similar) to automatically activate your dev environment when you enter your project's directory.
