# Machinefile GitHub Action


This action allows you to run Dockerfile/Containerfile commands directly on the host system without using Docker or any other container engine. It's useful for executing build commands in a predictable environment or setting up development tools.


## Usage

```yaml
steps:
- uses: actions/checkout@v3
- name: Run Machinefile commands
  uses: gbraad-redhat/machinefile-executor-action@v1
  with:
    containerfile: 'Containerfile'  # or path to your Containerfile
    context: '.'  # Build context directory
```

## Inputs

| Input         | Description                              | Required | Default        |
|---------------|------------------------------------------|----------|----------------|
| containerfile | Path to the Dockerfile/Containerfile     | Yes      | 'Containerfile'|
| context       | Directory to use as build context        | Yes      | '.'            |

## Example

Here's an example workflow that uses the Machinefile Executor to set up a development environment:

```yaml
name: Build with Containerfile

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Run Dockerfile commands
      uses: gbraad-redhat/machinefile-executor-action@v1
      with:
        dockerfile: 'containers/Containerfile-devtools'
        context: '.'
        
    - name: Run build tests
      run: |
        # Your build commands here
        make test
```


## License

[MIT License](LICENSE)


## Author

| [!["Gerard Braad"](http://gravatar.com/avatar/e466994eea3c2a1672564e45aca844d0.png?s=60)](http://gbraad.nl "Gerard Braad <me@gbraad.nl>") |
|---|
| [@gbraad](https://gbraad.nl/social) |