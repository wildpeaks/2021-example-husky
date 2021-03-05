# Example: Git Hooks

Example showing how to use [Husky](https://www.npmjs.com/package/husky)
to prevent commits that don't pass linters.

Warning: **it's possible to skip hooks** (by not installing dependencies or with a CLI flag),
so you shouldn't expect every commit to have been sanitized.

Also, [Husky v5 changed usage terms](https://dev.to/typicode/what-s-new-in-husky-5-32g5),
so you need to be a Sponsor if it's not for an open source project.


---
## You probably don't need this

Lint tests should also run server-side using Github Actions (and prevent merging to your main branch unless it passes tests),
so it might feel redundant to run it locally as well, especially when Husky makes every git hook slightly slower
even if you only want to use `pre-commit`.

Also, VSCode already has a great extensions:
 - [dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
 - [esbenp.prettier-vscode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)


---
## Example: Eslint

Lint the source code using [eslint](https://www.npmjs.com/package/eslint).

`package.json`:
````json
{
	"eslintConfig": {
		"extends": "@wildpeaks/commonjs"
	},
	"scripts": {
		"lint": "eslint src/**/*.js",
		"postinstall": "husky install"
	},
	"devDependencies": {
		"eslint": "...",
		"husky": "..."
	}
}
````

`.husky/pre-commit`:
````
npm run lint
````


---
## Example: Commitlint

Lint the commit message using [commitlint](https://www.npmjs.com/package/commitlint).

`package.json`:
````json
{
	"commitlint": {
		"extends": [
			"@commitlint/config-conventional"
		]
	},
	"scripts": {
		"postinstall": "husky install"
	},
	"devDependencies": {
		"@commitlint/cli": "...",
		"@commitlint/config-conventional": "...",
		"husky": "..."
	}
}
````

`.husky/commit-msg`:
````
npx commitlint -E HUSKY_GIT_PARAMS
````


---
## Example: Prettier

Reformat the source code using [prettier](https://www.npmjs.com/package/prettier)
and [pretty-quick](https://www.npmjs.com/package/pretty-quick).

`package.json`:
````json
{
	"prettier": "@wildpeaks/prettier-config",
	"scripts": {
		"postinstall": "husky install"
	},
	"devDependencies": {
		"husky": "...",
		"prettier": "...",
		"pretty-quick": "..."
	}
}
````

`.husky/pre-commit`:
````
npx pretty-quick --staged
````
