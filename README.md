# HeadlessUI Invalid Hook Test
simple repo built to demonstrate the `Invalid hook call` error i get when a monorepo contains two frontend apps that both depend on `@headless-ui/react`

## Reproducing Error
pull this repo and run
```bash
$ yarn
$ yarn --cwd app2 start
```
navigate to localhost:3000 with the console open and see that nothing loads + a whole mess of errors are thrown that seem to indicate that React is not being loaded correctly

note that running
```bash
$ yarn --cwd app1 start
```
results in a fully functional placholder app

## Variations

### Swap order 
1. update the root `package.json` "workspaces" property to be `"packages": ["app2", "app1"]`
2. delete the root `yarn.lock` file + reinstall via `yarn`
3. notice that now app2 runs fine, and app1 results in error

### Remove HeadlessUI dependency
1. remove the `@headless-ui/react` dependency from the `package.json` of the first app
2. delete the root `yarn.lock` file + reinstall via `yarn`
3. notice that now the second app runs fine (the first will no longer run b/c of the missing dependency)
