# Writing documentation

The Documentation is written using Markdown And it is really easy to get started.

You only need to work in the docs directory since everything is already configured and ready to go

---
You create a new page by simply creating a new `file.md` in the docs directory.
All the files in there are automatically added to the sidebar depending on the folder you put the file in.
You can further custumize the position label of your entries by creating a `_category_.json` file in this file you can customize the label of the folder, its position in the [sidebar](https://docusaurus.io/docs/next/sidebar) and add a link to it so when we press the folder in the sidebar we are greated with an auto generated interface that automatically adds all files in said category, You can manually add files to these categories as well for more information [read here on how to create a doc](https://docusaurus.io/docs/next/create-doc)
and [here](https://docusaurus.io/docs/next/sidebar#autogenerated-sidebar-metadata) on  autogenarating categories

## Setup Local Development

### Prerequisites

- [x] [Node Js](https://nodejs.org/en/download/) version >= 14 or above (which can be checked by running node -v).
- [x] [Yarn](https://yarnpkg.com/en/) version >= 1.5 (which can be checked by running yarn --version)

### Installation

```bash
git clone git@gitlab.com:carelyo/docs.git
cd docs && cd Carelyo Docs
yarn install
---
yarn start  Serves Documentation Portal on <http://localhost:3000>

```

## Issue Board

![board](board.png)
Your first step is to check the [issue board](https://gitlab.com/carelyo/docs/-/boards/3741305) this is where you will find and track all issues related to updating our documentations if the issue you are working on is not here create a new issue in the backlog add the `Docs` label issues that you begin with directly are added on the `In Progress` List.
Issues that you are not working on yet are added on todo if you plan to work on them soon or the backlog when they have lower priority. no more than 6 issues can be on `Todo` at any given time so if the `Todo` is full pick a task from there first and write your new task to the backlog.

### Linking Your Commits To Issues

You can link to an issue by mentioning it in you commit messages or merge requests with #issue_number `#12`
You can use keywords such as closes fix  resolve to automatically close an issue in from your commits or merge requests [read more](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically) and relations to other issue with the keyword relate , related to etc
Closed Issues are moved to `Closed` on the board.

## Commiting changes

When writing a commit message make sure it

- Contains enough information

- Prefix Your commit message with

  - Added for new documents
  - Changed for changes in present documents
  - Removed if you removed a document
  - fixed when you fix a document eg typos , style and so on

- Add Appropiate label to your merges and issues
- Use keywords to automatically close your issue

:::caution
Dont do one massive commit with lots of changes we will not merge such commits so do small and detailed commits that are related to an issue if no issue exist create one
:::

- You can commit changes  to [Develop Branch](https://gitlab.com/carelyo/docs/-/tree/develop/docs) or create your own "feature" branch then merge to develop

## Markdown Features

Documentation is one of your product's interfaces with your users. A well-written and well-organized set of docs helps your users understand your product quickly. Our aligned goal here is to help your users find and understand the information they need, as quickly as possible.

Docusaurus 2 uses modern tooling to help you compose your interactive documentation with ease. You may embed React components, or build live coding blocks where users may play with the code on the spot. [*Read More*](https://docusaurus.io/docs/next/markdown-features)

## Vscode Extensions

> [**Markdown lint**](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint).
>
>[**Markdown All in One**](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one).

---

:::info
We merge the develop branch  first to `Staging` at least once a week and create a `tag` when we merge
staging to `Main` which is at least once a month this is when we create a `release` when necessary.
:::

## Resources

---

- [Docusaurus Documentation](https://docsify.js.org/#/)
- [Prismjs Documentation](https://prismjs.com/index.html)
- [Gitlab Markdown Documentation](https://docs.gitlab.com/ee/user/markdown.html#gitlab-flavored-markdown)
- [Markdown Guide](https://www.markdownguide.org/basic-syntax/)

---

[Go to docs!](https://carelyo.gitlab.io/docs/#/)