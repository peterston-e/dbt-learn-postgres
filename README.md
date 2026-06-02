# dbt Local – Jaffle Shop (Postgres)

A local dbt learning project using the [jaffle-shop-classic](https://github.com/dbt-labs/jaffle-shop-classic) dataset, connected to a local PostgreSQL database. Based on the dbt Fundamentals course but running on Postgres instead of Snowflake or BigQuery.

---

## Prerequisites

- Python 3.12
- Homebrew
- PostgreSQL 16 (`brew install postgresql@16`)
- This repo cloned locally

---

## First time setup

### 1. Create and activate the virtual environment

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install dbt-core dbt-postgres
```

### 2. Configure your profiles.yml

Add the following to `~/.dbt/profiles.yml`:

```yaml
jaffle_shop:
  target: dev
  outputs:
    dev:
      type: postgres
      host: localhost
      user: dbt_user
      password: dbt_password
      port: 5432
      dbname: jaffle_shop
      schema: dbt_dev
      threads: 4
```

### 3. Set up the Postgres database

```bash
psql postgres
```

Then inside the Postgres shell:

```sql
CREATE DATABASE jaffle_shop;
CREATE USER dbt_user WITH PASSWORD 'dbt_password';
GRANT ALL PRIVILEGES ON DATABASE jaffle_shop TO dbt_user;
\q
```

---

## Each session

### Start Postgres

```bash
brew services start postgresql@16
```

### Activate the venv

```bash
source .venv/bin/activate
```

Your prompt will change to show `(.venv)` when active.

> **Note:** If `dbt` resolves to the wrong binary after activating, run `hash -r` to clear the shell cache.

### Stop Postgres when done

```bash
brew services stop postgresql@16
```

### Deactivate the venv

Only needed if switching environments in the same terminal session — closing the terminal or VS Code handles this automatically.

```bash
deactivate
```

---

## Running dbt

```bash
dbt debug      # test your connection
dbt seed       # load raw CSV data into Postgres
dbt run        # build all models
dbt test       # run tests
dbt clean      # remove compiled files
```

---

## Gotchas

- **CSV headers must be lowercase** — Postgres is case-sensitive. The seed files in `seeds/` use lowercase headers (`id`, `first_name` etc). If you ever re-download the raw CSVs from S3 the headers will be uppercase and seeding will fail.
- **Shell cache** — if `dbt` resolves to dbt-fusion instead of dbt-core after activating the venv, run `hash -r` to fix it.
- **Dropping seeds** — if you need to re-seed from scratch, drop the tables manually first or run `dbt seed --full-refresh`.

---

## Resources

- [dbt docs](https://docs.getdbt.com/docs/introduction)
- [dbt Discourse](https://discourse.getdbt.com/)
- [dbt Slack](http://slack.getdbt.com/)
- [jaffle-shop-classic repo](https://github.com/dbt-labs/jaffle-shop-classic)
