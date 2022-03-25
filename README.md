# Data Science in Production

My notes and codes as I work through the book **Data Science in Production: Building Scalable Model Pipelines with Python** by Ben G. Weber.

## Setup

For Python virtual environment, we will use pipenv.

### Install pipenv
```bash
python3 -m pip install pipenv
```

### Create virtual environment with pipenv
```bash
pipenv install --python 3.10
```

### Activate the virtual environment
```bash
pipenv shell
```

### Install python packages within activate virtual environment (example below)
```bash
pipenv install matplotlib
```

### Google Cloud command line tools (locally)

Set up the Google Cloud command line tools, in order to set up credentials for connecting to BigQuery. See this link for current release and specific OS: https://cloud.google.com/sdk/docs/install

```bash
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-378.0.0-darwin-arm.tar.gz

tar zxvf google-cloud-sdk-378.0.0-darwin-arm.tar.gz google-cloud-sdk

./google-cloud-sdk/install.sh
```

Once the Google Cloud command line tools are installed, we can
set up credentials for connecting to BigQuery:

```bash
gcloud config set project your_project_id
gcloud auth login
gcloud init
gcloud iam service-accounts create dsdemo
gcloud projects add-iam-policy-binding your_project_id
  --member "serviceAccount:dsdemo@your_project_id.iam.
            gserviceaccount.com" --role "roles/owner"
gcloud iam service-accounts keys
       create dsdemo.json --iam-account
       dsdemo@your_project_id.iam.gserviceaccount.com
export GOOGLE_APPLICATION_CREDENTIALS= /your-path/dsdemo.json
```