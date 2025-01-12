## CLI Install

<br>

#### NPM

```sh
npm create astro@latest
```

#### PNPM

```sh
pnpm create astro@latest
```

#### Yarn

```sh
yarn create astro
```


<br>

- If all goes well, you will see a success message followed by some recommended next steps.
<br>
- Now that your project has been created, you can `cd` into your new project directory to begin using Astro.
<br>
- If you skipped the “Install dependencies?” step during the CLI wizard, then be sure to install your dependencies before continuing.

<br>

## Install Dependencies

<br>

#### NPM

```sh
npm install
```

#### PNPM

```sh
pnpm install
```

#### Yarn

```sh
yarn install
```

<br>

---

<br>

## CLI Flags

`create-astro` automatically runs in _interactive_ mode, but you can also specify your project name and template with command line arguments.

<br>

#### NPM

```sh
npm create astro@latest my-astro-project -- --template minimal
```

#### yarn

```
yarn create astro my-astro-project --template minimal
```

#### PNPM

```
pnpm create astro my-astro-project --template minimal
```

<br>

#### Flag Table

May be provided in place of prompts

| Name                         | Description                                |
| :--------------------------- | :----------------------------------------- |
| `--help` (`-h`)              | Display available flags.                   |
| `--template <name>`          | Specify your template.                     |
| `--install` / `--no-install` | Install dependencies (or not).             |
| `--add <integrations>`       | Add integrations.                          |
| `--git` / `--no-git`         | Initialize git repo (or not).              |
| `--yes` (`-y`)               | Skip all prompts by accepting defaults.    |
| `--no` (`-n`)                | Skip all prompts by declining defaults.    |
| `--dry-run`                  | Walk through steps without executing.      |
| `--skip-houston`             | Skip Houston animation.                    |
| `--ref`                      | Specify an Astro branch (default: latest). |
| `--fancy`                    | Enable full Unicode support for Windows.   |


<br>

---

<br>

## Themes & Starter Templates

<br>

#### NPM Command

```sh
npm create astro@latest -- --template <example-name>
```

#### PNPM Command

```
pnpm create astro@latest --template <example-name>
```

#### Yarn Command

```
yarn create astro --template <example-name>
```

<br>

Found at: https://github.com/withastro/astro/tree/main/examples

- basics
- blog
- component
- container-with-vitest
- framework-alpine
- framework-preact
- framework-react
- framework-solid
- framework-svelte
- framework-vue
- hackernews
- integration
- minimal
- portfolio
- ssr
- starlog
- toolbar-app
- with-markdoc
- with-mdx
- with-nanostores
- with-tailwindcss
- with-vitest

<br>

---

<br>

## Add integrations

https://docs.astro.build/en/install-and-setup/#add-integrations

You can start a new astro project and install any [official integrations](https://docs.astro.build/en/guides/integrations-guide/) or community integrations that support the `astro add` command at the same time by passing the `--add` argument to the `create astro` command.

https://astro.build/integrations/