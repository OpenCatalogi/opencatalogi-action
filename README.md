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
      - name: Deploy Open Catalogi Github Page
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

> **Note**
> When you first run the workflow you need to `manually` activate github pages on your repository! Head over to setting -> pages. Select `deploy form a branch` as a source and `gh-pages` as your branche (unles you configured the page to be build in a differend branche)
> ![Page Settings](docs/page_settings.png)
> Afther pressing save head over tot the actions and take a look at the `pages build and deployment` action
> ![Page Action](docs/page_build.png)
> When it is done it will also tell you under wich link you can find your page
> ![Page Action done](docs/page_build_done.png)


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

## Tips
Besides making creating a frontend for your catalogue its also a goed idea to define how your organisation uses open source. Luckily this is verey easilly don by adding the publiccode action to your workflow 

````yaml
name: My PublicCode Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy Product Github Page
        uses: OpenCatalogi/productpage-action@1
      - name: Update opencatalogi.yaml
        uses: OpenCatalogi/publiccode-action@1
````

[Read more](https://github.com/marketplace/actions/create-or-update-publiccode-yaml) about the publiccode action that also creates the opencatalogi.yaml

## Working with branche protection
Keep in mind that this action creates/updates a file and force pushes into the beanche it was run on. It is therfore incompatible with github branche protection ON THE SAME branche. You can hower the wrokflow to start higher up in the branche tree to circumvent this. e.g. if you normaly work with a branche setup like:

- Master (protected)
- - Development (protected)
- - - Feature-1
- - - Feature-1

You can configure the workflow to trigger on

````yaml
on:
  push:
    branches:
      - 'feature-*'
````

The adjusted publiccode or opencatalogi files will then come allong in you normal pull requests from `feature-x` to `developement`etc.

## Special thanxs
As is the case with most software this action is based on the work of others, and uses there code. We would like to give a special shout out to the following parties and thier code

- [James Ives | github-pages-deploy-action#readme](https://github.com/JamesIves/github-pages-deploy-action#readme]).
- [SpicyPizza | create-envfile](https://github.com/SpicyPizza/create-envfile).

## Maintainers
This software is maintained by [Conduction b.v.](https://conduction.nl/)

## License
© 2023 Conduction B.V.

Licensed under the EUPL. The version control system provides attribution for specific lines of code.

## Remarks
This GitHub Action is published in the GitHub Marketplace. As such, you can find the [Terms of Service here](). Also, [here]() you can find the GitHub Marketplace Developer Agreement.
