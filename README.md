# dstack templates

This repo contains `dstack` template examples.

Currently, the scope of templates is limited to `dstack` UI:
  - `dstack` server accepts `DSTACK_TEMPLATES_REPO` environment variable pointing to a repo with templates.
  - Tempaltes are YAML files under `.dstack/templates` folder inside the repo.
  - Each template has `type` set to `wizard-template`, `id` (an identifier unique inside the repo), `title` (human-readable name of the template to be shown in the list of templates), `parameters`, and `configuration`.
  - Each parameter has `type` (enumeration supported by UI) and other properties supported by each parameter type.
  - `dstack` server returns templates via its REST endpoint `/api/templates/list` (response is a JSON array each item with the same schema as the YAML of the template).
  - The `New` drop-down button on the `Runs` page in `dstack` UI prompts the user to select a wizard template (if the REST endpoint returns any).
  - The UI wizard prompts the user to configure the parameters the wizard supports and applies them to `configuration`.

## Supported parameters

| Type               | Description                                                                   |
|--------------------|-------------------------------------------------------------------------------|
| `name`             | Allows to configure an optional run name.                                     |
| `ide`              | Allows to configure a desktop IDE (e.g. VS Code, Cursor, etc.).               |
| `resources`        | Allows to configure resources, etc.                                           |
| `python_or_docker` | Allows to configure either Python or Docker image.                            |
| `repo`             | Allows to optionally configure a repo.                                        |
| `working_dir`      | Allows to optionally configure a working dir.                                 |
| `env`              | Allows to configure additional environment variable. The special value `$random-password` tells the UI to automatically set the value by generating a random password.                         |