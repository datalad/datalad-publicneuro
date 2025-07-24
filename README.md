# DataLad PublicnEUro extension

This repository contains a datalad extension that simplifies data download
from PublicnEUro collections.


# Installation

Install the extension via pip (a virtual environment is recommended):

```bash
> pip install datalad-publicneuro
```

# Usage
The extension provides the new git annex special remote `uncurl-publicneuro`. To use it, activate the special remote in your DataLad dataset:

```bash
git annex initremote uncurl-publicneuro type=external externaltype=uncurl-publicneuro encryption=none
```

The `uncurl-publicneuro` special remote handles URLs with the following structure (where `<dataset-id>` is the PublicnEUro ID of the dataset, e.g., `PN000001`, and `path` is the absolute path of a file within the dataset, e.g., `/README.txt`):

```
publicneuro+https://<dataset-id><path>
```

The following command adds a reference to a file in a PublicnEUro dataset and downloads the file content (here the file `/README.txt` of dataset `PN000001` is added with the local name `README.txt`):

```bash
> git annex addurl --file README.txt publicneuro+https://PN000001/README.txt
```

The command will prompt for credentials if no credentials are available yet.
After successful authentication, the file will be downloaded and added to the annex.
Valid credentials will be stored in DataLad's credential store and automatically used for subsequent `addurl`-commands.

## Credentials on Windows

The DataLad credential system prompts for credentials that are not yet known.
On Windows the special remote might freeze, when prompting for credentials.
There are two ways to avoid this:

1. Use `datalad credentials set` to set the credentials for the authentication realm before adding or "getting" publicneuro URLs.
   The authentication realm for the PublicnEUro dataset `<dataset-id>` is `https://datacatalog.publicneuro.eu/<dataset-id>`.
   For example, the authentication realm for the dataset `PN000001` is `https://datacatalog.publicneuro.eu/PN000001`.

2. Use the environment variables `PUBLICNEURO_USER_<dataset-id>` and `PUBLICNEURO_PASSWORD_<dataset-id>` to set the credentials.
   For example, for the dataset `PN000001`, you can set the environment variables `PUBLICNEURO_USER_PN000001` and `PUBLICNEURO_PASSWORD_PN000001`.
   If both environment variables are set, the special remote will use them instead of DataLad's credential system and will not prompt for credentials.


# Contributing

PRs and issues are very welcome! Please open an issue or a pull request if you find a bug or have a feature request.
