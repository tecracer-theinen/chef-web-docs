This subcommand has the following options:

`-y`, `--yes`

:   Use to specify if the Chef Infra Server can go offline during
    tar.gz-based backups.

`--pg-options`

:   Specify additional options to pass to PostgreSQL during backups.

`-c`, `--config-only`

:   Backup the Chef Infra Server configuration **without** backing up data.

`-t`, `--timeout`

:   Set the maximum amount of time in seconds to wait for shell commands (default 600). This option should be set higher than 600 for backups taking longer than 10 minutes.

`-h`, `--help`

:   Show help message.
