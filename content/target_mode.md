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

- train
- Target IO
- supporting elements
- diagram

## Use

- `credential` file
- `chef-client -z -t <name>`
- configure a runner with different client configs in `/etc/chef/`

## Limitations

- linux-only
- problems with FFI, 3rd Party Gems, certain architectural patterns (e.g. Python Helper), Windows

## History

- 15.0.293 (May 2019)
- 15.1.36 (Jul 2019)
  - Reusing connections
  - new: `systemd_unit`, `log`, `ruby_block`, `breakpoint`
- 16.6.14 (Oct 2020)
  - Remote Ohai
- 18.0.169 (Oct 2022)
  - `rest_resource`
- 18.x (2024)
  - generic Target Mode
