# Infrastructure

![Starts in 2023](https://img.shields.io/badge/Started-2023-brightgreen)

This repo has everything I need to set up all my infrastructure.

## Getting Started

### Set up local environment

1. Install the required tools:

    - [go-task](https://taskfile.dev/)
    - [poetry](https://python-poetry.org/docs/)
    - [sops](https://github.com/getsops/sops)
    - [age](https://github.com/FiloSottile/age)

2. Install environment dependencies:

    ```shell
    task bootstrap:deps
    ```

### Bootstrap

1. Generate age key pairs. Using SOPS with Age allows us to encrypt secrets.

    ```shell
    age-keygen -o secrets/age.key
    ```

2. Create the `secret/bootstrap.sops.yaml` configuration file. Fill out the appropriate vars in `secret/bootstrap.sops.yaml`.

    ```shell
    # Decrypt bootstrap secrets
    task sops:decrypt -- secrets/bootstrap.sops.yaml
    # Encrypt bootstrap secrets
    task sops:encrypt -- secrets/bootstrap.sops.yaml
    ```

3. Once done run the following command which will verify and generate all the files needed to continue.

    ```shell
    task bootstrap:main
    ```

## LICENSE

[MIT](LICENSE)
