# How to use `ts/javascript` to create your own action

- Vist Github
- Go to [typescript-action](https://github.com/actions/typescript-action) and click `Use this template` button

!!! Note

    ```bash
    .
    ├── __test__    # testing
    ├── dist        # build distination folder
    ├── action.yml  # Action configuration file which contains the entry point for the action
    ├── src         # Action ts logical code
    ```

    - [actions/toolkit](https://github.com/actions/toolkit) the code library
    - [@actions/core](https://github.com/actions/toolkit/tree/main/packages/core) use to return value, logs, secret registration and expose varaibles bewteen actions.s
    - [@actions/exec](https://github.com/actions/toolkit/tree/main/packages/exec) used to exec command
    - [@actions/io](https://github.com/actions/toolkit/tree/main/packages/io) used to ooperate files.
    - [@actions/github](https://github.com/actions/toolkit/tree/main/packages/github) GitHub basic

- Install npm dependencies

  ```bash
    npm i <lib>
  ```

!!! note

    You can use _[js-action](https://github.com/actions/javascript-action)_ to generate the template.

- Examples

  [buildversion-action](https://github.com/nqerz/buildversion-action)

  the main logic of the structure is:

  ```bash
    ./src
    ├── context.ts        # Entry point of the mapping
    ├── fs-helper.ts      # File handling functions
    ├── main.ts           # Entry function
    ├── state-helper.ts   # state management functions
  ```

  workflow should contain `action` test jobs

  ```yaml
  test: # make sure the action works on a clean machine without building
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: ./
        id: BUILD_VERSION_NUMBER
        with:
          file-path: ${{ github.workspace }}/__tests__/version.properties
          run-number: ${{ github.run_number }}
      - run: echo ${{ steps.BUILD_VERSION_NUMBER.outputs.build_number }}
  ```

  others ref：[setup-go](https://github.com/actions/setup-go)

!!! note

    - change `scripts` -> `test`: npm run-script build && jest
    - prettier and vscode ts format conflict issue an be solved by configuring the rules of eslint, you can ask ChatGPT to get detail steps.
