<!-- Copyright Vespa.ai. Licensed under the terms of the Apache 2.0 license. See LICENSE in the project root. -->

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://assets.vespa.ai/logos/Vespa-logo-green-RGB.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://assets.vespa.ai/logos/Vespa-logo-dark-RGB.svg">
  <img alt="#Vespa" width="200" src="https://assets.vespa.ai/logos/Vespa-logo-dark-RGB.svg" style="margin-bottom: 25px;">
</picture>

# Visual Retrieval ColPali


# Developing

First, install `uv`:
  
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Then, in this directory, run:

```bash
uv sync --extra dev
```

This will generate a virtual environment with the required dependencies at `.venv`.

To activate the virtual environment, run:

```bash
source .venv/bin/activate
```

And run development server:

```bash
python hello.py
```

## Preparation

First, set up your `.env` file by renaming `.env.example` to `.env` and filling in the required values.
(Token can be shared with 1password, `HF_TOKEN` is personal and must be created at huggingface)
If you are just connecting to a deployed Vespa app, you can skip to [Connecting to the Vespa app](#connecting-to-the-vespa-app-and-querying).

### Deploying the Vespa app

To deploy the Vespa app, run:

```bash
python deploy_vespa_app.py --tenant_name mytenant --vespa_application_name myapp --token_id_write mytokenid_write --token_id_read mytokenid_read
```

You should get an output like:

```bash
Found token endpoint: https://abcde.z.vespa-app.cloud
````

### Feeding the data

#### Dependencies

In addition to the python dependencies, you also need `poppler`
On Mac:

```bash
brew install poppler
```

First, you need to create a huggingface token, after you have accepted the term to use the model at https://huggingface.co/google/paligemma-3b-mix-448.
Add the token to your environment variables as `HF_TOKEN`:

```bash
export HF_TOKEN=yourtoken
```

To feed the data, run:

```bash
python feed_vespa.py --vespa_app_url https://myapp.z.vespa-app.cloud --vespa_cloud_secret_token mysecrettoken
```

### Connecting to the Vespa app and querying

As a first step, until we hook up to frontend, you can run the `query_vespa.py` script to run some sample queries against the Vespa app:

```bash
python query_vespa.py
```
