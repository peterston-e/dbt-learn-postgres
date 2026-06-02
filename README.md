Welcome to your new dbt project!

## This is a Local setup you will need to activate the venv file

# dbt Local – Jaffle Shop (Postgres)

A local dbt project using the jaffle-shop-classic dataset, connected to a local PostgreSQL database.

## Prerequisites

- Python 3.12
- PostgreSQL installed and running locally
- This repo cloned locally

## First time setup

Create the virtual environment and install dependencies:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install dbt-core dbt-postgres
```

## Activating the environment

Run this at the start of each session before using dbt:

```bash
source .venv/bin/activate
```

Your prompt will change to show `(.venv)` when active.

## Deactivating the environment

Only needed if you want to exit the venv in the same terminal session:

```bash
deactivate
```

Closing the terminal or VS Code deactivates it automatically.

## Running dbt

```bash
dbt debug      # test your connection
dbt seed       # load raw CSV data into Postgres
dbt run        # build all models
dbt test       # run tests
```

### Resources:

- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](http://slack.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices
