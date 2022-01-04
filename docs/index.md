# Carelyo Documentation Portal

> Welcome to Carelyo Documentation Portal
> Here you can read about the careylyo web application
> Your first step should be setting up your`development` environment head to [Setup](setup.md) to get started

## Writing documentation

The Documentation is written using Markdown. So it really easy to get started.

---
You create a new page by simply creating a new `file.md` in the docs directory.
To show the page in the side menu you have to add it to the `_sidebar.md` file.

The side menu is essencially a markdown list.

```markdown
- Helpers
  - [Mutations](mutations.md)
  - [Queries](queries.md)
  - [Hooks](hooks.md)
  - [Utils](utils.md)
 
```

## CLI

#### Setup Local Development

```bash
npm i docsify-cli -g
git clone git@gitlab.com:carelyo/docs.git
cd docs
docsify serve ./docs
```

Serves Documentation Portal on <http://localhost:3000>

## Vscode Extensions

?> **markdownlint** VS Marketplace Link: <https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint>.

?> **Markdown All in One** VS Marketplace Link: VS Marketplace Link: <https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one>.

## GitPages

Commit your changes to [Develop Branch](https://gitlab.com/carelyo/docs/-/tree/develop/docs)

Do a `merge request` to main to push your changes to [Carelyo Documentation Portal](https://carelyo.gitlab.io/docs/#/)
