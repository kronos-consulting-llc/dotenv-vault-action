# Github Action - dotenv-vault-action

## Description

This action allows you to download `.env` files from [dotenv-vault](https://www.dotenv.org/) and use them in your
workflow.

## Usage

```yaml
- name: Download .env.production file and delete it after the workflow is finished
  uses: zdeneklapes/dotenv-vault-action@v2
  with:
    dotenvMe: ${{ secrets.DOTENV_ME }}
    stage: "production"
    delete: "true"
- name: Download .env.ci file and keep it after the workflow is finished
  uses: zdeneklapes/dotenv-vault-action@v2
  with:
    dotenvMe: ${{ secrets.DOTENV_ME }}
    stage: "ci"
    delete: "false"
- name: Your next step
  run: source .env.ci && echo $SOME_ENV_VAR_IN_CI
- name: Your next step
  run: source .env.production && echo $SOME_ENV_VAR_IN_PRODUCTION
```

## Inputs

### `dotenvMe` (required)
- **Description**: The `dotenvMe` secret from [dotenv-vault](https://www.dotenv.org/).

### `stage` (optional, default: 'ci')
The stage of the `.env` file you want to download.

**Examples**: `ci`/`staging`/`production`/`development` or any other stage you have set up in dotenv-vault.

### `delete` (optional, default: true)

- **Description**: If set to `false`, then all `.env*` files will be kept after the workflow is finished. By default, all `.env*` files are removed.
