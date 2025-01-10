## CLI Install

#### NPM

```sh
npm create astro@latest
```

#### With Yarn

```sh
yarn create astro
```

#### With PNPM:

```sh
pnpm create astro
```


<br>

- If all goes well, you will see a success message followed by some recommended next steps.
  
- Now that your project has been created, you can `cd` into your new project directory to begin using Astro.

- If you skipped the “Install dependencies?” step during the CLI wizard, then be sure to install your dependencies before continuing.

```sh
npm install
```

<br>

---

<br>

`create-astro` automatically runs in _interactive_ mode, but you can also specify your project name and template with command line arguments.

```sh
# npm
npm create astro@latest my-astro-project -- --template minimal

# yarn
yarn create astro my-astro-project --template minimal

# pnpm
pnpm create astro my-astro-project --template minimal
```


<br>

---

<br>

## Add integrations

https://docs.astro.build/en/install-and-setup/#add-integrations

You can start a new astro project and install any [official integrations](https://docs.astro.build/en/guides/integrations-guide/) or community integrations that support the `astro add` command at the same time by passing the `--add` argument to the `create astro` command.

Run the following command in your terminal, substituting any integration that supports the `astro add` command:

- [npm](https://docs.astro.build/en/install-and-setup/#tab-panel-24)
- [pnpm](https://docs.astro.build/en/install-and-setup/#tab-panel-25)
- [Yarn](https://docs.astro.build/en/install-and-setup/#tab-panel-26)

```sh
npm create astro@latest -- --add react --add tailwind
```