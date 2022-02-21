## {{ cookiecutter.project_name }} project!
---

_dbt version: 1.0.0_

### A. Setting up Python environment

- Set up Python environment for developing
    ```bash
    # Create Python virtual environment
    python -m venv path/to/your/venv

    # Install dependencies
    source path/to/your/venv/bin/activate
    pip install -U pip setuptools wheel
    pip install -r requirements.txt
    ```

### B. Dbt common operations

#### 1. Setting up

- Create your dbt profiles.yml for development following the file `profiles-dev.yml`
  - Refer: [Configure your profile](https://docs.getdbt.com/dbt-cli/configure-your-profile)

- Install dbt dependencies

    ```bash
    dbt deps
    ```

- Check connection

    ```bash
    dbt debug
    ```

#### 2. Generate dbt source, base model YAML files

- Create source YAML file

    ```bash
    dbt run-operation generate_source --args '{"name": "your_source_name", "schema_name": "your_schema_name"}'
    ```

- Create base models

    ```bash
    dbt run-operation generate_base_model --args '{"source_name": "your_source_name", "table_name": "your_table_name"}'
    ```

- Create model YAML file

    ```bash
    dbt run-operation generate_model_yaml --args '{"model_name": "model_name_to_create_yaml"}'
    ```

- Refer: [dbt-codegen](https://github.com/dbt-labs/dbt-codegen#generate_model_yaml-source)
#### 3. Run models

- Run normal models

    ```bash
    dbt run -m model_name_or_tag_or_state
    ```

- Run snapshot models

    ```bash
    dbt snapshot -s snapshot_name
    ```

#### 4. Test models

- Run dbt tests

    ```bash
    dbt test -m model_name_or_tag_or_state
    ```

- Check required tests (Refer: [dbt-meta-testing](https://hub.getdbt.com/tnightengale/dbt_meta_testing/latest/))

    ```bash
    dbt run-operation required_tests
    ```

### C. Linting

- Lint code with

    ```bash
    sqlfluff lint path/to/file/or/folder
    ```

- Auto fix code

    ```bash
    sqlfluff fix path/to/file/or/folder
    ```

- Refer: [sqlfluff](https://github.com/sqlfluff/sqlfluff)

### C. Pre-commit hook

- Install pre-commit hooks

    ```bash
    pre-commit install
    ```

- Uninstall pre-commit hooks

    ```bash
    pre-commit uninstall
    ```

- Refer: [pre-commit](https://pre-commit.com/)

### D. Github CI

- To use Github Action workflows:
  - Create folder `.github/workflows`
  - Copy Github Action workflow files from the folder `.github/workflow-templates` to the newly-created folder
  - Set up Github Action following usage guide in each workflow file

- Available workflows:
  - **pr_to_master**: triggered at every PR to the main branch, do linting code, checking tests, running delta models & testing (dev)
  - **push_to_master**: triggered at commit push to the main branch, do checking tests, running delta models & testing (prod)
  - **full_refresh_prod**: triggered manually or every 6 hours, do running all models & testing

### E. Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](https://community.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices
