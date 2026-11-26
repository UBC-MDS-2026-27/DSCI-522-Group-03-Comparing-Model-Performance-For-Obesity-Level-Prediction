# Contributing to the Obesity Level Predictor project

This outlines how to propose a change to the Obesity Level Predictor project.

### Fixing typos

Small typos or grammatical errors in documentation may be edited directly using
the GitHub web interface, so long as the changes are made in the _source_ file.

*  YES: you edit the Quarto source file `reports/obesity-prediction.qmd`.
*  NO: you edit the rendered `reports/obesity-prediction.html` or `.pdf`.

### Prerequisites

Before you make a substantial pull request, you should always file an issue and
make sure someone from the team agrees that it's a problem. If you've found a
bug, create an associated issue with type "Bug" and illustrate the bug with a minimal reproducible example.

### Setting up the project

We develop in the same Docker container that users run the analysis in, so
everyone uses the same software and package versions. First follow the
[Usage section of the README](README.md#usage) (install Docker, clone the
repository, make an ssh key, and download the image). Run all the commands
below from the root of this repository.

### Working in the container

We edit and run the code inside the container by connecting
[Positron](https://positron.posit.co/) to it over ssh. Your project folder is
shared with the container at `/workspace`, so a file you change there changes
on your computer too.

<details>
<summary><strong>Once, before your first connection</strong></summary>

1. Install [Positron](https://positron.posit.co/download.html). Its Remote SSH
   feature comes built in, so you don't need an extension.
2. Make sure you have an ssh key at `~/.ssh/id_ed25519.pub` and have downloaded
   the image with `docker compose pull` (both covered in the
   [README](README.md#usage)).
3. Check that Git knows who you are on your computer:

   ``` bash
   git config --global user.email
   ```

   This should print the email of your GitHub account. If it prints nothing, set
   your name and email:

   ``` bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

   `docker-compose.yml` shares these settings with the container, so your
   commits made there count as yours.

</details>

<details>
<summary><strong>Each time you work on the project</strong></summary>

1. In a terminal, in your project folder, start the container in the background:

   ``` bash
   docker compose up -d
   ```

   `docker compose ps` should list `analysis-env` as running.
2. In Positron, open the Command Palette (Cmd+Shift+P on Mac, Ctrl+Shift+P on
   Windows), run **Remote SSH: Show Remote Menu**, and pick **Connect to Host**.
3. Type `root@localhost:2222` and press Enter. A new Positron window opens.
   *  If it asks for the platform of the remote host, pick **Linux**.
   *  If it asks whether you trust the host (a "fingerprint"), click **Continue**.
   *  The first time, Positron installs its server inside the container. This
      can take several minutes.
4. Open the project folder. The bottom left corner shows `SSH: localhost:2222`,
   but the Explorer says *No folder opened*. Click **Open Folder**, delete what is
   in the path box, type `/workspace`, and press Enter (you may need to click OK
   more than once). The window reloads and the Explorer shows
   `WORKSPACE [SSH: LOCALHOST:2222]` with the project files.
5. Pick the interpreter (check this every time). Click the interpreter button
   at the top right, then **New Console Session…**, and choose
   **Python 3.14 (uv: dsci-522-group-03-comparing-model-performance-for-obesity-level-prediction)**
   with the path `/opt/venv/bin/python`. If it isn't listed, run
   **Python: Select Interpreter** from the Command Palette, choose
   **Enter interpreter path…**, and type `/opt/venv/bin/python`.
   Do not pick `/usr/bin/python3` (the container's system Python) or
   `/workspace/.venv` (an environment from your own computer, which doesn't run
   in the container). To check, run this in the Console:

   ``` python
   import sys; print(sys.executable)
   ```

   It should print `/opt/venv/bin/python`.
6. Work as usual. The Terminal, Console and Render button all run inside the
   container.
7. When you are done, close the Positron window, then stop the container in a
   terminal on your computer:

   ``` bash
   docker compose down
   ```
</details>

<details>
<summary><strong>If it doesn't connect</strong></summary>

*  **`~/.ssh/id_ed25519.pub` is a folder:** Docker created it because the key
   didn't exist yet. Run `docker compose down`, delete that folder, make the key
   (see the [README](README.md#usage)), and start again.
*  **`~/.gitconfig` is a folder, or Git in the container doesn't know your
   name:** the same thing happened with your Git settings. Run
   `docker compose down`, delete that folder, set your name and email (step 3
   above), and start again.
*  **GitHub asks you to sign in when you push from the container:** sign in once
   in the browser window Positron opens. Positron remembers it.
*  **It asks for a password:** the container can't see your key. Check that your
   key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.
*  **"Remote host identification has changed":** you are using a new image. Run
   `ssh-keygen -R "[localhost]:2222"`, then connect again.
*  **ssh refuses the key on Windows or Linux:** sshd wants `root` to own the key
   file, but the mounted one belongs to you. Our Dockerfile already turns this
   check off (`StrictModes no`), so make sure you have pulled the latest image
   with `docker compose pull`.
*  **Port 2222 is already in use:** change the first `2222` in
   `docker-compose.yml` to another number (e.g. `2223`), and connect to that
   port instead.

</details>

To re-run the analysis and render the report without opening the container:

``` bash
docker compose run --rm analysis-env uv run quarto render
```

### Adding or updating a package

1. On a new branch, add the package with an exact version:

   ``` bash
   uv add <package>==<version>
   ```

   This pins the version in `pyproject.toml` and updates `uv.lock`.
2. Commit the changed `pyproject.toml` and `uv.lock` together and push them.
   GitHub Actions then builds and publishes a new image on Docker Hub, and
   commits the new `sha-` tag to the `image:` line of `docker-compose.yml` on
   your branch.
3. When the workflow finishes, get that commit and download the new image:

   ``` bash
   git pull
   docker compose pull
   ```

4. Merge the branch into `main` in a pull request. The merge builds the image
   once more and commits a new tag to `main`. When that run finishes, everyone
   runs `git pull` on `main` and `docker compose pull` again.

### Publishing the report

The report on [GitHub Pages](https://ubc-mds-2026-27.github.io/DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction/)
is a copy of the rendered report in `docs/index.html`. Each time you re-render
the report, copy it there again, then commit and push:

``` bash
cp reports/obesity-prediction.html docs/index.html
```

### Pull request process

*  Create a new Git branch for each pull request (PR), starting from an
   up-to-date `main`. Do not commit directly to `main`.
*  Give the branch a short name that describes the work,
   for example `fix-readme-typo` or `add-eda-figure`.
*  Keep each branch small: one independent piece of work per branch.
*  Before opening the PR, render the report (`uv run quarto render`)
   to check that the analysis still runs from start to finish.
*  Open a PR into `main` and describe what changed and why.
   Link the related issue (e.g., "Closes #12").
*  At least one other team member must review and approve the PR before it is merged.
   The reviewer, not the author, merges it.
*  New code should follow the PEP8 [style guide](https://peps.python.org/pep-0008/).

### Code of Conduct

Please note that this project is released with a [Contributor Code of
Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to
abide by its terms.

### Use of AI

Contributors may use generative AI tools for debugging, checking code, and limited guidance on
the analysis (e.g., suggesting approaches or explaining methods), but analysis decisions and the
content of work remain their own. Every contributor must understand and verify any AI-assisted
work before submitting it. Humans will open all issues and pull requests and make all final merge
decisions. Keep track of the AI use, including example prompts, for the AI use statement
in the README.

### Attribution

These contributing guidelines were adapted from the [dplyr contributing guidelines](https://github.com/tidyverse/dplyr/blob/master/.github/CONTRIBUTING.md) and the [Breast Cancer Predictor](https://github.com/UBC-MDS/DSCI_522_project-template-breast-cancer-predictor/blob/1.0.0/CONTRIBUTING.md)
example project.