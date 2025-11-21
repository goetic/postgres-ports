# Postgres Ports Tree

This ports overlay provides versions of Postgres and associated packages,
allowing users to pick a specific version.

## Usage

Add the public key for the pkg repo, to ensure that signatures are properly
validated:

``` shell
cat <<'EOF' > /usr/local/etc/pkg/repos/postgres.conf
beam: {
  url: "https://goetic-pkg.s3.us-east-2.amazonaws.com/postgres/freebsd/${ABI}/latest",
  signature_type: "pubkey",
  pubkey: "/usr/local/etc/ssl/postgres-ports.pub",
  enabled: yes
}
EOF
```

``` shell
cat <<'EOF' > /usr/local/etc/ssl/postgres-ports.pub
-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAzRpocI3URq965dK7l3p2
sEOKWwA+J1HTrbdG+K4VCNfB2b8tui37sp8Q24OMknfJixvey/kVEhWemN6cLHrV
Uj5qHOfTKm8kdAaZKaMDQxnVi2fqP36Sbrfm5Ln2uU6Nd3168sOt6STCKjfv3OKU
Evv+ltQ5q06G5sbTIU9Sl+B69/rnIjjELzyqmmb7/u93Ispgf+MlEUTxJi2Gl1ki
2dMuuGJopo1zGOD+j0CIeSIUVYuhl6uN4QKUz30FZjMpFOGd4gvR9K5VC9FghHcp
YFKefsWUaGlfisfwM4ZSa9VKymwVtREvdUbe/7J9az7c7BEgdTQMDlMyeOUEe9mt
CtztuxAB/WzwnCvnNmepda/7372U6ijlCLO6/9+kwX/yX72G6IioBZ1DZh4NS5eM
UV1Yd65ce0JrCtASYgoGrsmo1ch6NMOWbRguLG60H32vGgpbIAN6oLmLpFdbmlvq
LurZVf+2qvusX7vZN1sA77qePWWtcKgslrRvN3IN9eMGnd42rs0cNjsB8J8VqLPL
DGOapzEq8d01hlDWSSpBBW1xoi90aql0vXhjN2kqxtK7ZuNsY1514TTomv2hubYl
l5tyuSbQ1rG/6SPZblXI6u/roZoZIZ6zQ3H6x4pnaq/2Y56kpG0bR2eGs6YX0uwM
qLtzysaWPOVJ/Qp4daWoUnECAwEAAQ==
-----END PUBLIC KEY-----
EOF
```

``` shell
pkg update
pkg search pgbackrest
```

## Development

``` shell
poudreire jail -c -j 143amd64 -v 14.3-RELEASE -a amd64
poudreire jail -c -j 143aarch64 -v 14.3-RELEASE -a arm64.aarch64

poudriere ports -c
poudriere ports -c -f postgres -m null -M /workspace/github/goetic/postgres-ports -p postgres
```

``` shell
poudriere bulk -j 143amd64 -O postgres -f packages-default
```

``` shell
poudriere pkgclean -A -j <jail>
poudriere logclean -a -j <jail>
```
