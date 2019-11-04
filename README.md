# makefiles

Makefiles for wrapping different types of projects.

## Available Makefiles

Each Makefile should be in its own directory.

| Project Type | Description                             |
| ------------ | --------------------------------------- |
| terraform    | Targets for common Terraform operations |

## Usage

Each Makefile has built-in help, debugging, and info commands that should cover
all usage. You can using the following commands:

| Command      | Description                        |
| ------------ | ---------------------------------- |
| `make`       | Alias for `make help`              |
| `make help`  | Prints basic help for all commands |
| `make debug` | Prints vars used in the Makefile   |
| `make info`  | Print metadata about the module    |
