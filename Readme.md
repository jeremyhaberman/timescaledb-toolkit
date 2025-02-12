[![CI](https://github.com/timescale/timescaledb-toolkit/actions/workflows/ci.yml/badge.svg)](https://github.com/timescale/timescaledb-toolkit/actions/workflows/ci.yml)


# TimescaleDB Toolkit #

This repository is the home of the TimescaleDB Toolkit team. Our mission is to
ease all things analytics when using TimescaleDB, with a particular focus on
developer ergonomics and performance. Our issue tracker contains more
on [the features we're planning to work on](https://github.com/timescale/timescaledb-toolkit/labels/proposed-feature)
and [the problems we're trying to solve](https://github.com/timescale/timescaledb-toolkit/labels/feature-request),
and our [Discussions forum](https://github.com/timescale/timescaledb-toolkit/discussions) contains ongoing conversation.

Documentation for this version of the TimescaleDB Toolkit extension can be found
in this repository at [`docs`](https://github.com/timescale/timescaledb-toolkit/tree/main/docs).


## 🖥 Try It Out ##

The extension comes pre-installed on all [Timescale Cloud](https://www.timescale.com/products#timescale-cloud) instances and also on our full-featured [`timescale/timescaledb-ha` docker image](https://hub.docker.com/r/timescale/timescaledb-ha). 

If DEB and RPM packages are a better fit for your situation, refer to the [Install Toolkit on self-hosted TimescaleDB](https://docs.timescale.com/timescaledb/latest/how-to-guides/hyperfunctions/install-toolkit/#install-toolkit-on-self-hosted-timescaledb) how-to guide for further instructions on installing the extension via your package manager.

All versions of the extension contain experimental features in the `toolkit_experimental` schema. See [our docs section on experimental features](/docs/README.md#tag-notes) for more details.

## 💿 Installing From Source ##

### Supported platforms

The engineering team regularly tests the extension on the following platforms:

- x86_64-unknown-linux-gnu (Ubuntu Linux 20.04) (tested prior to every merge)
- x86_64-apple-darwin (MacOS 12) (tested frequently on eng workstation)
- aarch64-apple-darwin (MacOS 12) (tested frequently on eng workstation)

aarch64-unknown-linux-gnu support is [in development](https://github.com/timescale/timescaledb-toolkit/issues/382).

As for other platforms:  patches welcome!

### 🔧 Tools Setup ###

Building the extension requires valid [rust](https://www.rust-lang.org/), [rustfmt](https://github.com/rust-lang/rustfmt), and clang installs, along with the postgres headers for whichever version of postgres you are running, and pgx.
We recommend installing rust using the [official instructions](https://www.rust-lang.org/tools/install):
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
and build tools, the postgres headers, in the preferred manner for your system. You may also need to install OpenSSl.
For Ubuntu you can follow the [postgres install instructions](https://www.postgresql.org/download/linux/ubuntu/) then run
```bash
sudo apt-get install make gcc pkg-config clang postgresql-server-dev-14 libssl-dev
```
and finally, [pgx](https://github.com/tcdi/pgx), which can be installed with
```bash
cargo install --version '=0.4.5' cargo-pgx && cargo pgx init --pg14 pg_config
```

Installing from source is also available on macOS and requires the same set of prerequisites and set up commands listed above.

### 💾 Building and Installing the extension ###

Download or clone this repository, and switch to the `extension` subdirectory, e.g.
```bash
git clone https://github.com/timescale/timescaledb-toolkit && \
cd timescaledb-toolkit/extension
```
Then run
```
cargo pgx install --release && \
cargo run --manifest-path ../tools/post-install/Cargo.toml -- pg_config
```

To initialize the extension afer installation, star enter the following into `psql`:
```
CREATE EXTENSION timescaledb_toolkit;
```

## ✏️ Get Involved ##

The TimescaleDB Toolkit project is still in the initial planning stage as we
decide our priorities and what to implement first. As such, now is a great time
to help shape the project's direction! Have a look at the
[list of features we're thinking of working on](https://github.com/timescale/timescaledb-toolkit/labels/proposed-feature)
and feel free to comment on the features, expand the list, or
hop on the [Discussions forum](https://github.com/timescale/timescaledb-toolkit/discussions) for more in-depth discussions.

### 🔨 Testing ###

See above for prerequisites and installation instructions.

You can run tests against a postgres version `pg12`, `pg13`, or `pg14` using

```
cargo pgx test ${postgres_version}
```


## 🐯 About TimescaleDB

**[TimescaleDB](https://github.com/timescale/timescaledb)** is a
**distributed time-series database built on PostgreSQL** that scales to
over 10 million of metrics per second, supports native compression,
handles high cardinality, and offers native time-series capabilities,
such as data retention policies, continuous aggregate views,
downsampling, data gap-filling and interpolation.

TimescaleDB also supports full SQL, a variety of data types (numerics,
text, arrays, JSON, booleans), and ACID semantics. Operationally mature
capabilities include high availability, streaming backups, upgrades over
time, roles and permissions, and security.

TimescaleDB has a **large and active user community** (tens of millions
of downloads, hundreds of thousands of active deployments, Slack channels
with thousands of members).
