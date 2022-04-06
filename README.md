# Carelyo Documentation

Welcome to Carelyo! [Go to docs!](https://carelyo.gitlab.io/docs/#/)

## Setup Local Development
This section describes what you need to do to setup your working environment

1. [x] Setup Gitlab with SSH key: Go to docs > Getting Started > Get Started > Setup Gitlab SSH Key
2. [x] Setup docker compose for running backend api server: [Click here](https://gitlab.com/carelyo/docker-compose) and follow the instructions carefully
3. [x] Request access to Figma: [Request Figma Access](https://gitlab.com/carelyo/docs/-/issues/new). Enter a title and Assign it to **Micheal Ulasi**
4. [x] Register yourself as **Active Student** (only **Students or Interns**). [GetStarted]

### Prerequisites

- [x] [Node Js](https://nodejs.org/en/download/) version >= 14 or above (which can be checked by running node -v).
- [x] [Yarn](https://yarnpkg.com/en/) version >= 1.5 (which can be checked by running yarn -v)
- [x] [npm](https://www.npmjs.com/) version >= 1.4.29 (which can be checked by running npm -v)

### Installation

```bash
git clone git@gitlab.com:carelyo/docs.git
cd docs && cd Carelyo Docs
yarn install
---
yarn start  Serves Documentation Portal on <http://localhost:3000>
or
npm start Serves Documentation Portal on <http://localhost:3000>
```

## Issue Board

![board](board.png)
Your first step is to check the [issue board](https://gitlab.com/carelyo/docs/-/boards/3741305) this is where you will
find and track all issues related to updating our documentations if the issue you are working on is not here create a
new issue in the backlog add the `Docs` label issues that you begin with directly are added on the `In Progress` List.
Issues that you are not working on yet are added on todo if you plan to work on them soon or the backlog when they have
lower priority. No more than 6 issues can be on `Todo` at any given time so if the `Todo` is full pick a task from there
first and write your new task to the backlog.

### Linking Your Commits To Issues

You can link to an issue by mentioning it in you commit messages or merge requests with #issue_number `#12`
You can use keywords such as closes fix resolve to automatically close an issue in from your commits or merge
requests [read more](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
and relations to other issue with the keyword relate , related to etc Closed Issues are moved to `Closed` on the board.

## Commiting changes

When writing a commit message make sure it

- Contains enough information

- Prefix Your commit message with

  - Added for new documents
  - Changed for changes in present documents
  - Removed if you removed a document
  - fixed when you fix a document eg. typos, style and so on

- Add Appropiate label to your merges and issues
- Use keywords to automatically close your issue

:::caution Dont do one massive commit with lots of changes we will not merge such commits so do small and detailed
commits that are related to an issue if no issue exist create one
:::

- You can commit changes to [Develop Branch](https://gitlab.com/carelyo/docs/-/tree/develop/docs) or create your own "
  feature" branch then merge to develop

## Markdown Features

Documentation is one of your product's interfaces with your users. A well-written and well-organized set of docs helps
your users understand your product quickly. Our aligned goal here is to help your users find and understand the
information they need, as quickly as possible.

Docusaurus 2 uses modern tooling to help you compose your interactive documentation with ease. You may embed React
components, or build live coding blocks where users may play with the code on the spot. [*Read
More*](https://docusaurus.io/docs/next/markdown-features)

## Vscode Extensions

> [**Markdown lint**](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint).
>
>[**Markdown All in One**](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one).

---

:::info We merge the develop branch first to `Staging` at least once a week and create a `tag` when we merge staging
to `Main` which is at least once a month this is when we create a `release` when necessary.
:::

## Resources

---

- [Docusaurus Documentation](https://docsify.js.org/#/)
- [Prismjs Documentation](https://prismjs.com/index.html)
- [Gitlab Markdown Documentation](https://docs.gitlab.com/ee/user/markdown.html#gitlab-flavored-markdown)
- [Markdown Guide](https://www.markdownguide.org/basic-syntax/)

---

[Go to docs!](https://carelyo.gitlab.io/docs/#/)
