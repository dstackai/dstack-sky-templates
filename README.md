# dstack templates

This repo contains `dstack` template examples.

Currently, the scope of templates is limited to `dstack` UI:
  - `dstack` server accepts `DSTACK_SERVER_TEMPLATES_REPO` environment variable pointing to a git repo with templates.
  - Templates are YAML files under `.dstack/templates` folder inside the repo.
  - Each template has `type` set to `template`, `name` (unique inside the repo), `title` (human-readable name of the template to be shown in the list of templates), `parameters`, and `configuration` (the dstack run configuration).
  - Each parameter has `type` (enumeration supported by UI) and other properties supported by each parameter type.
  - `dstack` server returns templates via a per-project REST endpoint `POST /api/project/{project_name}/templates/list` (response is a JSON array, each item with the same schema as the YAML of the template).
  - The `New` drop-down button on the `Runs` page in `dstack` UI prompts the user to select a template (if the REST endpoint returns any).
  - The UI prompts the user to configure the parameters the UI supports and applies them to `configuration`.

> **Note:** Server-wide templates (configured via `DSTACK_SERVER_TEMPLATES_REPO`) are the first step.
> Per-project template configuration will come in a future iteration.

For inspiration on building a visual template editor, see the [dstack Configuration Editor](https://dstack-template-editor.thinkcoder.sky.dstack.ai/)
by [@deep-diver](https://github.com/deep-diver) ([repo](https://github.com/deep-diver/dstack-template)).

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