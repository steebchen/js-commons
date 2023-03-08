# abinnovision/js-commons

Commonly used configs, etc. for the JavaScript ecosystem
within [AB innovision](https://github.com/abinnovision). This repository is
structured as a monorepo, which emits multiple packages, which are defined in
the [packages](./packages) directory.

## Packages

Currently, the following packages exist:

* [eslint-config-base](./packages/eslint-config-base): ESLint config which acts
	as base for all others, can be used standalone for Javascript only.
* [eslint-config-typescript](./packages/eslint-config-typescript): ESLint config
	for Typescript related projects.
* [eslint-config-react](./packages/eslint-config-react): ESLint config for React
	related projects.
* [prettier-config](./packages/prettier-config): Shared Prettier config for all
	projects.
* [commitlint-config](./packages/commitlint-config): Shared Commitlint config or
	all projects.

All packages are published under the `@abinnovision`-scope to the GitHub
Packages Registry. _See here for a guide on how to set up the Private Registry
on
your local machine:
[abinnovision/commons#private-npm-registry](https://github.com/abinnovision/commons/blob/master/topics/private-npm-registry.md)_

## ESLint

ESLint is a popular open-source static code analysis tool for JavaScript. It is
used to analyze and identify common coding errors, stylistic issues, and
potential bugs in your JavaScript code. ESLint is highly configurable and
supports a wide range of plugins and rule sets to meet the specific needs of
your
project.

Using ESLint in your project can help you maintain a consistent coding style,
improve code quality, and catch errors before they cause issues in production.
By integrating ESLint into your development workflow, you can ensure that your
code adheres to best practices and industry standards, making it easier to read,
debug, and maintain.

For the [AB innovision](https://github.com/abinnovision) organization we use a
custom shared ESLint config, which is split into three parts. Each part takes
care about a specific technology (e.g. Typescript, React). The configurations
can (sometimes must) be used on conjunction with each other.

As we always (at least should) use Prettier in conjunction with ESLint, we must
disable code style formatting in ESLint.
The [eslint-config-prettier](https://www.npmjs.com/package/eslint-config-prettier)
comes to rescue for this case.

### Javascript

For plain Javascript projects, the following config will be used:

* [@abinnovision/eslint-config-base](./packages/eslint-config-base)

_(This section just exists for the sake of completeness. We should never use
plain
Javascript for new projects, always prefer Typescript.)_

Example configuration in the `package.json`:

```json5
{
	// ...
	"eslintConfig": {
		"extends": [
			"@abinnovision/base",
			"prettier"
		]
	},
	// ...
}
```

#### Installation

```shell
yarn add --dev \
	@abinnovision/eslint-config-base \
	eslint eslint-plugin-import \
	eslint-config-prettier
```

### Typescript

For Typescript only projects, the following configs will be used:

* [@abinnovision/eslint-config-base](./packages/eslint-config-base)
* [@abinnovision/eslint-config-typescript](./packages/eslint-config-typescript)

Example configuration in the `package.json`:

```json5
{
	// ...
	"eslintConfig": {
		"extends": [
			"@abinnovision/base",
			"@abinnovision/typescript",
			"prettier"
		]
	},
	// ...
}
```

#### Installation

```shell
yarn add --dev \
	@abinnovision/eslint-config-base @abinnovision/eslint-config-typescript \
	eslint eslint-plugin-import \
	@typescript-eslint/eslint-plugin @typescript-eslint/parser \
	eslint-config-prettier
```

### Typescript React

For Typescript & React projects, the following configs will be used:

* [@abinnovision/eslint-config-base](./packages/eslint-config-base)
* [@abinnovision/eslint-config-typescript](./packages/eslint-config-typescript)
* [@abinnovision/eslint-config-react](./packages/eslint-config-react)

Example configuration in the `package.json`:

```json5
{
	// ...
	"eslintConfig": {
		"extends": [
			"@abinnovision/base",
			"@abinnovision/typescript",
			"@abinnovision/react",
			"prettier"
		]
	},
	// ...
}
```

#### Installation

```shell
yarn add --dev \
	@abinnovision/eslint-config-base @abinnovision/eslint-config-typescript @abinnovision/eslint-config-react \
	eslint eslint-plugin-import \
	@typescript-eslint/eslint-plugin @typescript-eslint/parser \
	eslint-plugin-react \
	eslint-config-prettier
```

## Prettier

Prettier is a popular open-source code formatting tool for various programming
languages, including JavaScript, TypeScript, CSS, and HTML. It is used to
automatically format your code according to a set of predefined rules, which can
help to ensure consistency and readability across your codebase.

Using Prettier in your project can save time and effort, as you no longer need
to manually format your code or worry about adhering to specific style guides.
Prettier automatically formats your code as you write it, making it easier to
maintain a consistent code style across your team or organization.

For the [AB innovision](https://github.com/abinnovision) organization we use a
custom shared Prettier config. This config package also comes with a compatible
EditorConfig.

The following package use used for the Prettier config:

* [@abinnovision/prettier-config](./packages/prettier-config)

Example configuration in the `package.json`:

```json5
{
	// ...
	"prettier": "@abinnovision/prettier-config"
	// ...
}
```

To synchronize the `.editorconfig` file from this package use the following:

```shell
yarn sync-editorconfig
```

Optionally, you can put it into your `postinstall` hook to always keep in sync
with the one defined in this project.

```json5
{
	// ...
	"scripts": {
		// ...
		"postinstall": "sync-editorconfig"
	},
	// ...
}
```

### Installation

```shell
yarn add --dev @abinnovision/prettier-config 
```

## Commitlint

Commitlint is a popular open-source tool used to enforce consistent commit
message formatting in Git repositories. It can be used to ensure that commit
messages follow a specific format, contain all the required information, and
provide a clear and concise summary of the changes made.

Using Commitlint in your project can help to improve the quality of your commit
messages, making it easier to track changes and understand what has been done in
each commit. It can also help to enforce specific commit message guidelines or
standards, such as those used in semantic versioning or Conventional Commits.

For the [AB innovision](https://github.com/abinnovision) organization we use a
custom shared Commitlint config.

The following package use used for the Commitlint config:

* [@abinnovision/commitlint-config](./packages/commitlint-config)

Example configuration in the `package.json`:

```json5
{
	// ...
	"commitlint": {
		"extends": ["@abinnovision/commitlint-config"]
	}
	// ...
}
```

### Installation

```shell
yarn add --dev @abinnovision/commitlint-config 
```
