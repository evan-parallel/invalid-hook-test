# HeadlessUI Invalid Hook Test
simple repo built to demonstrate the `Invalid hook call` error i get when a monorepo contains two frontend apps using different versions of React that both depend on `@headless-ui/react`

## Reproducing Error
pull this repo and run
```bash
$ yarn
$ yarn --cwd app-17 start
```
navigate to localhost:3000 with the console open and see that nothing loads + a whole mess of errors are thrown that seem to indicate that React is not being loaded correctly

note that running
```bash
$ yarn --cwd app-18-1 start
```
results in a fully functional placholder app

## Variations

### Swap order 
1. update the root `package.json` "workspaces.packages" property to be `"packages": ["app-17", "app18-1"]`
2. delete the root `yarn.lock` file + reinstall via `yarn`
3. notice that now app-17 runs fine, and app-18-1 results in error

### Remove HeadlessUI dependency
1. remove the `@headless-ui/react` dependency from the `package.json` of the first app in "workspaces.packages"
2. delete the root `yarn.lock` file + reinstall via `yarn`
3. notice that now the second app runs fine (the first will no longer run b/c of the missing dependency)

### Use Same React Version 
1. update the root `package.json` "workspaces.packages" property to be `"packages": ["app-18-2", "app18-1"]`
2. delete the root `yarn.lock` file + reinstall via `yarn`
3. notice that both apps now run as expected
4. we can also remove the "workspaces.nohoist" property from the root `package.json` and both apps should still continue working fine
