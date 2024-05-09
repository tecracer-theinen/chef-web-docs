+++
title = "About Target Mode"
draft = false
gh_repo = "chef-web-docs"
aliases = ["/target_mode.html"]
product = ["client"]

[menu]
  [menu.infra]
    title = "About Target Mode"
    identifier = "chef_infra/target_mode/introduction.md About Target Mode"
    parent = "chef_infra/target_mode"
    weight = 10
+++

## Introduction

- purpose
- problems solved
- focus audience/devices

## Architecture

- `train` framework
- Remote Ohai
- `shell_out`, `which`
- Target IO abstraction layer
- supporting elements(?)
- add architectural diagram

## Use

- `credential` file
- `chef-client --target <name>`
  - optional `--local-mode` for serverless operations
- configure a runner with different client configs in `/etc/chef/` for server integration

## Limitations

- AIX/BSD/Linux/Solaris-only, Mac OS X and Windows later
- problems with FFI, 3rd Party Gems, certain architectural patterns (e.g. local Python Helper), Windows DLL usage
- `only_if`/`not_if` only works with Ruby blocks, if you use the `TargetIO::` prefix and only supported functions

## Write Custom Resources for Target Mode

- toggle support flag in `provides` by adding `, target_mode: true`
- prefer `shell_out` calls to IO
- for IO calls prefix `TargetIO::` after checking remote-capable implementation
- methods from IO classes like `File`, `FileUtil`, etc which do not perform IO can stay unprefixed
- avoid using `ruby_block` as these will always run locally

## History

- 15.0.293 (May 2019)
- 15.1.36 (Jul 2019)
  - Reusing connections
  - new: `systemd_unit`, `log`, `ruby_block`, `breakpoint`
- 16.6.14 (Oct 2020)
  - Remote Ohai
- 18.0.169 (Oct 2022)
  - `rest_resource`
- 18.9.0 (2024)
  - generic Target Mode
