# Open Catalogi action
This action builds on organisation specific Open Catalogi page as static github page.|

## Usage
To use this action, simply include it as a step in your workflow file. No inputs are required.

````yaml
name: My Open Catalogi Workflow

on:
  schedule:
    - cron: '0 0 * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Update publiccode.yaml
        uses: OpenCatalogi/opencatalogi-action@latest
````

In the above example an page is created or updated every night at 0:00, we advise this route becouse you will autmaticly suplied with fixes and new features. You can however also choose other options to trigger a page build

To trigger a page build whenever you commit something to the main  branche
````yaml
on:
  push:
    branches:
      - main
````

To gain a bit more control and only trigger a page build manually usw
````yaml
on:
  workflow_dispatch:
````
> **Warning**
> If you do not supply the action with an access token or an SSH key, you must access your repositories settings and provide `Read and Write Permissions` to the provided `GITHUB_TOKEN`, otherwise you'll potentially run into permission issues. Alternatively you can set the following in your workflow file to grant the action the permissions it needs.

```yml
permissions:
  contents: write
```

## Input

| Input Name                          | Description                                                                   | Default Value                                                            |
|------------------------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| `github_pages_branch`               | The branch on which the GitHub page will be built (Optional)                | `gh-pages`                                                               |
| `github_repository_name_as_prefix`  | Whether to use the GitHub repository name as a prefix (Optional)             | `true`                                                                   |
| `repository`                        | The GitHub repository to use (could be an external repository) (Optional)   | `github.event.repository.url`                                            |
| `me_url`                            | The profile URL used (Optional)                                            | `https://api.opencatalogi.nl/api/users/me`                                |
| `api_url`                           | The location of the Open Catalogi API (change if you are running your own API) (Optional) | `https://api.opencatalogi.nl/api`                          |
| `admin_url`                         | The admin (dashboard) URL used (Optional)                                   | `https://api.opencatalogi.nl/admin`                                       |
| `base_url`                          | The BASE location of the Open Catalogi API (change if you are running your own API) (Optional) | `https://api.opencatalogi.nl`                          |
| `frontend_url`                      | The location (URL) of this Open Catalogi installation (Optional)            | `https://api.opencatalogi.nl`                                            |
| `login_redirect`                    | The path for login redirection (Optional)                                  | `vault`                                                                  |
| `admin_dashboard_url`               | The location of the Open Catalogi dashboard (Optional)                      | `https://admin.opencatalogi.nl`                                          |
| `nl_design_theme_classname`         | The class name of the desired NL design theme (Optional)                   | `open-webconcept-theme`                                                  |
| `arrow_breadcrumbs`                 | Whether to use arrow breadcrumbs instead of the normal breadcrumbs (Optional) | `false`                                                             |
| `navbar_logo`                       | A base64 encoded SVG file or URL to the logo used in the main menu (Optional)| `https://openwebconcept.nl/wp-content/themes/openwebconcept/assets/src/images/logo@2x.png` |
| `gitname`                           | Git name configuration for bump commit (Optional)                            | `Open Catalogi bot`                                                     |
| `gitmail`                           | Git mail configuration for bump commit (Optional)                            | `bot@opencatalogi.nl`                                                   |


## Output

| Output Name     | Description                                                              |
|-----------------|--------------------------------------------------------------------------|
| `page`          | A zip of the build page                                                 |

## Special thanxs
As is the case with most software this action is based on the work of others, and uses there code. We would like to give a special shout out to the following parties and thier code

- [James Ives | github-pages-deploy-action#readme](https://github.com/JamesIves/github-pages-deploy-action#readme]).
- [SpicyPizza | create-envfile](https://github.com/SpicyPizza/create-envfile).

## Maintainers
This software is maintained by the Developers Italia team.

## License
© 2022 Gemeente Rotterdam

Licensed under the EUPL. The version control system provides attribution for specific lines of code.

## Remarks
This GitHub Action is published in the GitHub Marketplace. As such, you can find the [Terms of Service here](). Also, [here]() you can find the GitHub Marketplace Developer Agreement.
