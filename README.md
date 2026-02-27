# Test::PostgreSQL::v2

A modern PostgreSQL runner for Perl tests.

## Why v2?

The original [**Test::PostgreSQL**](https://metacpan.org/dist/Test-PostgreSQL) has several issues on modern Linux (Ubuntu 24.04+):
1. It looks for `postmaster` instead of `postgres`.
2. It tries to use system directories for sockets, leading to permission errors.
3. It doesn't handle modern "postgres" user role requirements well.

[**Test::PostgreSQL::v2**](https://metacpan.org/dist/Test-PostgreSQL-v2) fixes these by using isolated temporary directories for sockets,
providing automatic binary discovery, and allowing flexible host/user configuration.

## Usage with [Test::DBIx::Class](https://metacpan.org/dist/Test-DBIx-Class)

```perl
use Test::More;
use Test::DBIx::Class {
    schema_class => 'MyApp::Schema',
    traits       => ['Testpostgresqlv2'],
    deploy_db    => 1,
}, qw/:resultsets/;

ok my $user = ResultSet('User')->create({ name => 'John' }), 'Created user';
is $user->name, 'John', 'Name persisted correctly';

done_testing;
```
