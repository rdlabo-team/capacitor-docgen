# @rdlabo/capacitor-docgen

Generate Capacitor plugin documentation that includes members inherited through TypeScript
`extends`. Independently maintained fork of Ionic's
[`@capacitor/docgen`](https://github.com/ionic-team/capacitor-docgen).

## Try it in a small sandbox

```sh
mkdir docgen-demo
cd docgen-demo
npm init -y
npm install --save-dev @rdlabo/capacitor-docgen@0.4.1
```

Do not install upstream `@capacitor/docgen` in the same project; both publish the `docgen` binary.

Create `src/definitions.ts`:

```ts
export interface SharedOptions {
  requestId?: string;
}

export interface CreateOptions extends SharedOptions {
  value: string;
}

export interface MyPlugin {
  create(options: CreateOptions): Promise<void>;
}
```

Create `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true
  },
  "files": ["src/definitions.ts"]
}
```

Create `README.md` with the placeholders that docgen updates:

```md
<docgen-index></docgen-index>

<docgen-api></docgen-api>
```

Run:

```sh
npx docgen --project tsconfig.json --api MyPlugin --output-readme README.md --output-json dist/docs.json
```

The generated `CreateOptions` documentation includes both `value` and `requestId`. Edit the
TypeScript interfaces or JSDoc to change generated content; prose outside the markers stays.
Re-run the same command after edits.

For an existing plugin workflow, you can add a `package.json` script such as
`"docgen": "docgen --api MyPlugin --output-readme README.md"`. It is optional for this sandbox.

## Documentation

- [Differences from Upstream](./docs/upstream-differences.md)

<!-- rdlabo-docs-omit -->
**Full documentation:** [https://docs.rdlabo.dev/projects/capacitor-docgen](https://docs.rdlabo.dev/projects/capacitor-docgen)

## CLI

The easiest way to run `docgen` is to install `@rdlabo/capacitor-docgen` as a dev dependency
and add the command to the `package.json` scripts. In the example below, 
`HapticsPlugin` is the primary interface:

```bash
docgen --api HapticsPlugin --output-readme README.md
```

| Flag              | Alias | Description                                                                              |
|-------------------|-------|------------------------------------------------------------------------------------------|
| `--api`           | `-a`  | The name of the primary application programming interface. **Required**                  |
| `--output-readme` | `-r`  | Path to the markdown file to update. Note that the file must already exist. **Required** |
| `--output-json`   | `-j`  | Path to write the raw docs data as a json file.                                          |
| `--project`       | `-p`  | Path to the project's `tsconfig.json` file, same as the [project](https://www.typescriptlang.org/docs/handbook/compiler-options.html) flag for TypeScript's CLI. By default it'll attempt to find this file. |


#### package.json script

```json
{
  "scripts": {
    "docgen": "docgen --api HapticsPlugin --output-readme README.md"
  }
}
```

## API

The same API that's available to the CLI can also be imported from `@rdlabo/capacitor-docgen`.


## Related

- [Capacitor](https://capacitorjs.com/)
- [Capacitor Community Plugins](https://github.com/capacitor-community)
<!-- /rdlabo-docs-omit -->

<!-- rdlabo-docs-omit -->
## Maintainers

- [rdlabo](https://rdlabo.dev/)
<!-- /rdlabo-docs-omit -->
