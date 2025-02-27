# Contributing

First of all, thank you for contributing to Meilisearch! The goal of this document is to provide everything you need to know in order to contribute to Meilisearch and its different integrations.

<!-- MarkdownTOC autolink="true" style="ordered" indent="   " -->

- [Hacktoberfest](#hacktoberfest-2022)
- [Assumptions](#assumptions)
- [How to Contribute](#how-to-contribute)
- [Development Workflow](#development-workflow)
- [Git Guidelines](#git-guidelines)
- [Release Process (for internal team only)](#release-process-for-internal-team-only)

<!-- /MarkdownTOC -->

## Hacktoberfest 2022

It's [Hacktoberfest month](https://hacktoberfest.com)! 🥳

Thanks so much for participating with Meilisearch this year!

1. We will follow the quality standards set by the organizers of Hacktoberfest (see detail on their [website](https://hacktoberfest.com/participation/#spam)). Our reviewers will not consider any PR that doesn’t match that standard.
2. PRs reviews will take place from Monday to Thursday, during usual working hours, CEST time. If you submit outside of these hours, there’s no need to panic; we will get around to your contribution.
3. There will be no issue assignment as we don’t want people to ask to be assigned specific issues and never return, discouraging the volunteer contributors from opening a PR to fix this issue. We take the liberty to choose the PR that best fixes the issue, so we encourage you to get to it as soon as possible and do your best!

You can check out the longer, more complete guideline documentation [here](https://github.com/meilisearch/.github/blob/main/Hacktoberfest_2022_contributors_guidelines.md).

## Assumptions

1. **You're familiar with [GitHub](https://github.com) and the [Pull Request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) (PR) workflow.**
2. **You've read the Meilisearch [documentation](https://docs.meilisearch.com) and the [README](/README.md).**
3. **You know about the [Meilisearch community](https://docs.meilisearch.com/learn/what_is_meilisearch/contact.html). Please use this for help.**

## How to Contribute

1. Make sure that the contribution you want to make is explained or detailed in a GitHub issue! Find an [existing issue](https://github.com/meilisearch/meilisearch-symfony/issues/) or [open a new one](https://github.com/meilisearch/meilisearch-symfony/issues/new).
2. Once done, [fork the meilisearch-symfony repository](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) in your own GitHub account. Ask a maintainer if you want your issue to be checked before making a PR.
3. [Create a new Git branch](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-and-deleting-branches-within-your-repository).
4. Review the [Development Workflow](#development-workflow) section that describes the steps to maintain the repository.
5. Make the changes on your branch.
6. [Submit the branch as a PR](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork) pointing to the `main` branch of the main meilisearch-symfony repository. A maintainer should comment and/or review your Pull Request within a few days. Although depending on the circumstances, it may take longer.<br>
 We do not enforce a naming convention for the PRs, but **please use something descriptive of your changes**, having in mind that the title of your PR will be automatically added to the next [release changelog](https://github.com/meilisearch/meilisearch-symfony/releases/).

## Development Workflow

### Using Composer

#### Setup

You can set up your local environment natively or using `docker`, check out the [`docker-compose.yml`](/docker-compose.yml).

Example of running all the checks with docker:
```bash
docker-compose run --rm package bash -c "composer install && composer test:unit && composer lint:check"
```

To install dependencies:

```sh
composer install
```

#### Tests and Linter

Each Pull Request should pass the tests, and the linter to be accepted.

```sh
# Tests
docker run -p 7700:7700 getmeili/meilisearch:latest meilisearch --master-key=masterKey --no-analytics
composer test:unit
# Linter
composer lint:check
# Linter (with auto-fix)
composer lint:fix
# PHPstan
composer phpstan
```

### Using the Docker Environment

These commands do not work on MacOS, see [this issue](https://github.com/meilisearch/meilisearch-symfony/issues/6).

#### Setup

You can set up your local environment natively or using `docker`, check out the [`docker-compose.yml`](/docker-compose.yml).

Example of running all the checks with docker:
```bash
docker-compose run --rm package bash -c "list of the commands required to build + run tests + run linters"
```

To install dependencies:

To start and build your Docker environment, just execute the next command in a terminal:

```sh
docker-compose up -d
```

Be sure no other Meilisearch instance is currently running on your machine.

#### Tests and Linter

Each Pull Request should pass the tests, and the linter to be accepted.

```sh
# Tests
docker-compose exec -e MEILISEARCH_HOST=http://meilisearch:7700 php composer test:unit
# Linter
docker-compose exec php composer lint:check
# Linter (with auto-fix)
docker-compose exec php composer lint:fix
```

## Git Guidelines

### Git Branches

All changes must be made in a branch and submitted as PR.
We do not enforce any branch naming style, but please use something descriptive of your changes.

### Git Commits

As minimal requirements, your commit message should:
- be capitalized
- not finish by a dot or any other punctuation character (!,?)
- start with a verb so that we can read your commit message this way: "This commit will ...", where "..." is the commit message.
  e.g.: "Fix the home page button" or "Add more tests for create_index method"

We don't follow any other convention, but if you want to use one, we recommend [this one](https://chris.beams.io/posts/git-commit/).

### GitHub Pull Requests

Some notes on GitHub PRs:

- [Convert your PR as a draft](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/changing-the-stage-of-a-pull-request) if your changes are a work in progress: no one will review it until you pass your PR as ready for review.<br>
  The draft PR can be very useful if you want to show that you are working on something and make your work visible.
- The branch related to the PR must be **up-to-date with `main`** before merging. Fortunately, this project [integrates a bot](https://github.com/meilisearch/integration-guides/blob/main/resources/bors.md) to automatically enforce this requirement without the PR author having to do it manually.
- All PRs must be reviewed and approved by at least one maintainer.
- The PR title should be accurate and descriptive of the changes. The title of the PR will be indeed automatically added to the next [release changelogs](https://github.com/meilisearch/meilisearch-symfony/releases/).

## Release Process (for internal team only)

Meilisearch tools follow the [Semantic Versioning Convention](https://semver.org/).

### Automation to Rebase and Merge the PRs

This project integrates a bot that helps us manage pull requests merging.<br>
_[Read more about this](https://github.com/meilisearch/integration-guides/blob/main/resources/bors.md)._

### Automated Changelogs

This project integrates a tool to create automated changelogs.<br>
_[Read more about this](https://github.com/meilisearch/integration-guides/blob/main/resources/release-drafter.md)._

### How to Publish the Release

⚠️ Before doing anything, make sure you got through the guide about [Releasing an Integration](https://github.com/meilisearch/integration-guides/blob/main/resources/integration-release.md).

Make a PR modifying the file [`src/MeiliSearchBundle.php`](/src/MeiliSearchBundle.php) with the right version.

```php
VERSION = 'X.X.X'
```

Once the changes are merged on `main`, you can publish the current draft release via the [GitHub interface](https://github.com/meilisearch/meilisearch-symfony/releases): on this page, click on `Edit` (related to the draft release) > update the description (be sure you apply [these recommandations](https://github.com/meilisearch/integration-guides/blob/main/resources/integration-release.md#writting-the-release-description)) > when you are ready, click on `Publish release`.

A WebHook will be triggered and push the new package to [Packagist](https://packagist.org/packages/meilisearch/search-bundle).

<hr>

Thank you again for reading this through, we can not wait to begin to work with you if you made your way through this contributing guide ❤️
