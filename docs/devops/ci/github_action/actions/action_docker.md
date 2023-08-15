# How to use Docker to create your own action

- Vist Github
- Go to [hello-world-docker-action](https://github.com/actions/hello-world-docker-action) and click `Use this template` button

- Examples

  [buildversion-docker-action](https://github.com/znqerz/buildversion-docker-action)

  the main logic of the structure is:

  ```bash
  .
  ├── Dockerfile
  ├── LICENSE
  ├── README.md
  ├── action.yml
  ├── entrypoint.sh
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
          file-path: ./version.properties
          run-number: ${{ github.run_number }}
      - run: echo ${{ steps.BUILD_VERSION_NUMBER.outputs.build_number }}
  ```

  !!! note

Actions based on Docker should make sure workspace _mount path_
