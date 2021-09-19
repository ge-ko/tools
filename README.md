# Handy tools

A bunch of handy tools that I use in my every day work.

After you clone the folder, put it in the path for convenience.

## db

```shell
❯ db
database=> select * from table;
...
database=> \q

❯ db -- -c "select * from table" \
        -P pager=off --no-align -F $'\t' -P footer=off > pid-org.tsv

❯ db --help
DESCRIPTION
  Starts a database client

SYNOPSIS
  db [options] [--] [arg ...]

OPTIONS:

  Option          Parameter       Usage
  --------------  --------------  --------------------------------------------
  -h|--help                       Show this help
  -C|--context    <context>       Kubernetes context. Inferred from kubectl.
  -i|--image      <image>         Database client image.
  -c|--command    psql|pgdump|... Command to execute. Default: psql.
  -h|--host       <host>          Database host.
  -d|--database   <database>      Database name.
  -U|--user       <user>          Database user.
  -p|--port       <port>          Database port. Defaut: 5432.
  --              <args>          Additional arguments passed to the command.

EXIT STATUS:
  Returns success unless an invalid option is given.
```

## jwt-decode

```shell
❯ JWT_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

❯ echo $JWT_TOKEN | jwt-decode
HEADER
{
  "alg": "HS256",
  "typ": "JWT"
}
PAYLOAD
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
INVALID SIGNATURE
```

## functions

```shell
function epoch2date() { TZ=UTC date -d "@$1" -Iseconds }
function date2epoch() { TZ=UTC date -d "$1" +%s }
function base64encode() { echo -n "$1" | base64 }
function base64decode() { echo "$1" | base64 -d }
function waitup() { until ping -c1 $1 >/dev/null 2>&1; do :; done }
```