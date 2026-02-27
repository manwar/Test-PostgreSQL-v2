# Test::PostgreSQL::v2

A modern PostgreSQL runner for Perl tests.

## Why v2?

The original `Test::PostgreSQL` has several issues on modern Linux (Ubuntu 24.04+):
1. It looks for `postmaster` instead of `postgres`.
2. It tries to use system directories for sockets, leading to permission errors.
3. It doesn't handle modern "postgres" user role requirements well.

`Test::PostgreSQL::v2` fixes these by using isolated temporary directories for sockets,
providing automatic binary discovery, and allowing flexible host/user configuration.

## Usage with Test::DBIx::Class

```perl
use Test::PostgreSQL::v2;

our $pg;
BEGIN { $pg = Test::PostgreSQL::v2->new() }

use Test::DBIx::Class {
    connect_info => [ $pg->dsn, $pg->user, '' ],
    deploy_db    => 1,
}, 'MyResultSet';
```
