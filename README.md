# tool-sops

SOPS encryption utilities for the homelab infrastructure.

## encrypt_yaml_in_place

Encrypts a plaintext YAML file using SOPS + AGE, producing a `.sops.yaml` file.

### Usage

From a submodule directory:

```bash
cd app-copyparty
source .env  # Sets SOPS_AGE_KEY_FILE
../tool-sops/encrypt_yaml_in_place kubernetes/config.secret.yaml
```

### Options

| Flag | Description |
|------|-------------|
| `-f, --force` | Skip .yaml extension check |

### Features

- **Smart change detection**: Compares decrypted existing file with input; skips if unchanged
- **Safe operation**: Creates backup before encryption, restores on failure
- **Clear output**: Reports "already up-to-date" or shows diff of changes

### Requirements

- `sops` CLI installed
- `SOPS_AGE_KEY_FILE` environment variable set (typically via `source .env`)
- Input file must end with `.yaml` (unless `-f` is used)

### How It Works

1. Validates input file exists and has `.yaml` extension
2. If encrypted file exists, decrypts and compares with input
3. If changed (or new), encrypts input → `<name>.sops.yaml`
4. Plaintext input file remains on disk (gitignored)

## encrypt_json_in_place

Encrypts a plaintext JSON file using SOPS + AGE, producing a `.sops.json` file.

### Usage

From a submodule directory:

```bash
cd nodes
source .env  # Sets SOPS_AGE_KEY_FILE
../tool-sops/encrypt_json_in_place meshcommander-computerlist.json
```

### Options

| Flag | Description |
|------|-------------|
| `-f, --force` | Skip .json extension check |

### Features

- **Smart change detection**: Compares decrypted existing file with input; skips if unchanged
- **Safe operation**: Creates backup before encryption, restores on failure
- **Clear output**: Reports "already up-to-date" or shows diff of changes

### Requirements

- `sops` CLI installed
- `SOPS_AGE_KEY_FILE` environment variable set (typically via `source .env`)
- Input file must end with `.json` (unless `-f` is used)

### How It Works

1. Validates input file exists and has `.json` extension
2. If encrypted file exists, decrypts and compares with input
3. If changed (or new), encrypts input → `<name>.sops.json`
4. Plaintext input file remains on disk (gitignored)

## encrypt_tfstate_in_place

Encrypts a Terraform state file using SOPS + AGE, producing a `.tfstate.sops.json` file.

### Usage

```bash
cd terraform
source .env  # Sets SOPS_AGE_KEY_FILE
../tool-sops/encrypt_tfstate_in_place terraform.tfstate
```

### Options

| Flag | Description |
|------|-------------|
| `-f, --force` | Skip .tfstate extension check |

### Features

- **Smart change detection**: Compares decrypted existing file with input; skips if unchanged
- **Safe operation**: Creates backup before encryption, restores on failure
- **Clear output**: Reports "already up-to-date" or shows diff of changes

### Requirements

- `sops` CLI installed
- `SOPS_AGE_KEY_FILE` environment variable set (typically via `source .env`)
- Input file must end with `.tfstate` (unless `-f` is used)
- `terraform/.sops.yaml` with `encrypted_regex: ^(.*)$` to encrypt all fields

### How It Works

1. Validates input file exists and has `.tfstate` extension
2. If encrypted file exists, decrypts and compares with input
3. If changed (or new), encrypts input → `<name>.tfstate.sops.json`
4. Plaintext input file remains on disk (gitignored)

# Author

[Cameron King](http://cameronking.me)

# License

This software is released under the ISC license.

See `LICENSE` file for details.
