# CURATION-VSCODE-INTEGRATIONS
These dots provide project code integration with VS Code post DC-1820.

1) `.env` - defines the environmental variables for running tests.  Currently tests are run within the host's virtual env.  This is a vscode limitation.

2) `.vscode` contains the `launch.json` and `tasks.json` files for running curation in docker.  Furthermore, `settings.json` defines the configuration for running python tests (discovery, execution, and debugging)

## Configuration
For the `.env` file, fill out the following information.

Personal details:
```
USERNAME=<FIRST_INITIAL_LASTNAME>
GH_USERNAME=<GITHUB_USERNAME>
```

The following path variables must point to host locations.  `PYTHONPATH` must point to the `data_steward` folder (an incorrect path will cause project import errors during test execution).
```
GOOGLE_APPLICATION_CREDENTIALS=/PATH/TO/CREDENTIALS/aou-res-curation-test.json
PYTHONPATH=/PATH/TO/PROJECT/curation/data_steward
```

Define buckets and datasets:
```
DRC_BUCKET_NAME=<YOUR_NAME>_drc
BUCKET_NAME_FAKE=<YOUR_NAME>_fake
BUCKET_NAME_NYC=<YOUR_NAME>_nyc
BUCKET_NAME_PITT=<YOUR_NAME>_pitt
BUCKET_NAME_CHS=<YOUR_NAME>_chs
BUCKET_NAME_UNIONED_EHR=<YOUR_NAME>_drc

BIGQUERY_DATASET_ID=<YOUR_NAME>_ehr
RDR_DATASET_ID=<YOUR_NAME>_rdr
COMBINED_DATASET_ID=<YOUR_NAME>_combined
UNIONED_DATASET_ID=<YOUR_NAME>_unioned
COMBINED_DEID_DATASET_ID=<YOUR_NAME>_deid
```

Setting up `tasks.json` **only requires personal details, dataset names, and bucket names**.
```
"env": {
    // These values are configured for the container environment
    // and should not be modified
    "PYTHONPATH": "/home/curation/project/curation/curation_venv/lib/python3.7/site-packages",
    "GOOGLE_APPLICATION_CREDENTIALS": "/home/curation/project/curation/aou-res-curation-test.json",
    "APPLICATION_ID": "aou-res-curation-test",
    "GOOGLE_CLOUD_PROJECT": "aou-res-curation-test",
    "VOCABULARY_DATASET": "vocabulary20201008",
    // These values are for you to configure
    "GH_USERNAME": "<GITHUB_USERNAME>",
    "USERNAME": "<FIRST_INITIAL_LASTNAME>",
    "DRC_BUCKET_NAME": "<YOUR_NAME>_drc",
    "BUCKET_NAME_FAKE": "<YOUR_NAME>_fake",
    "BUCKET_NAME_NYC": "<YOUR_NAME>_nyc",
    "BUCKET_NAME_PITT": "<YOUR_NAME>_pitt",
    "BUCKET_NAME_CHS": "<YOUR_NAME>_chs",
    "BUCKET_NAME_UNIONED_EHR": "<YOUR_NAME>_drc",
    "BIGQUERY_DATASET_ID": "<YOUR_NAME>_ehr",
    "RDR_DATASET_ID": "<YOUR_NAME>_rdr",
    "COMBINED_DATASET_ID": "<YOUR_NAME>_combined",
    "UNIONED_DATASET_ID": "<YOUR_NAME>_unioned",
    "COMBINED_DEID_DATASET_ID": "<YOUR_NAME>_deid"
}
```

finally, define your entrypoint in `tasks.json`:

```
"python": {
    // Define your entrypoint here
    // NOTE: this is a path within the container.
    // It must start with /home/curation/project/curation/
    "file": "/home/curation/project/curation/data_steward/main.py",
}
```
