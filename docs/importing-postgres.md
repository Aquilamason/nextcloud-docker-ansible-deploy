# Importing an existing Postgres database from another installation (optional)

Run this if you'd like to import your database from a previous installation.
(don't forget to restore your data files in `/nextcloud/nextcloud-data/data` as well).


## Prerequisites

For this to work, **the database name in Postgres must match** what this playbook uses.
This playbook uses a Postgres database name of `nextcloud` by default (controlled by the `nextcloud_postgres_db_name` variable).
If your database name differs, be sure to change `nextcloud_postgres_db_name` to your desired name and to re-run the playbook before proceeding.

The playbook supports importing Postgres dump files in **text** (e.g. `pg_dump > dump.sql`) or **gzipped** formats (e.g. `pg_dump | gzip -c > dump.sql.gz`).

Importing multiple databases (as dumped by `pg_dumpall`) is also supported.

Before doing the actual import, **you need to upload your Postgres dump file to the server** (any path is okay).


## Importing

To import, run this command (make sure to replace `<server-path-to-postgres-dump.sql>` with a file path on your server):

```sh
ansible-playbook -i inventory/hosts setup.yml \
--extra-vars='server_path_postgres_dump=<server-path-to-postgres-dump.sql>' \
--tags=import-postgres
```

**Note**: `<server-path-to-postgres-dump.sql>` must be a file path to a Postgres dump file on the server (not on your local machine!).
