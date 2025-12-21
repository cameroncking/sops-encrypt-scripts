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
4. Removes plaintext input file on success

# Author

[Cameron King](http://cameronking.me)

# License

This software is released under the ISC license.

See `LICENSE` file for details.