# README

## Overview

A custom filter for Sceptre for unquoting resolvers appearing in var files.

## Installation

Installation instructions

To install directly from PyPI
```shell
pip install jinja-unquote-resolvers-filter
```

To install from the git repo
```shell
pip install git+https://github.com/Sceptre/jinja-unquote-resolvers-filter.git
```

## Usage/Examples

Refer to the [Sceptre resolver docs](https://docs.sceptre-project.org/latest/docs/filters.html#filters) <!-- This page does not exist yet. -->
for more information.

In your var file:

```yaml
Subnets:
  - '!stack_output_external mystack::subnet_a'  # Quotes needed to protect a YAML tag.
  - '!stack_output_external mystack::subnet_b'

VPC: '!stack_output_external mystack::vpc_id'
```

In your config:

```yaml
j2_environment:
  extensions:
    - jinja_unquote_resolvers_filer.UnquoteResolversFilterExtension

sceptre_user_data:
  subnets:
    {{ var.Subnets | unquote_resolvers(output_indent=4) | trim }}
  vpc: {{ var.VPC }}  # This filter not needed if the quoted resolvers are passed in scalars.
```

## License

Apache 2.0
