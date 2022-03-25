# Datasets

## Google Cloud command line tools on AWS EC2

Install the Google Cloud library and other python packages by running the following:
```bash
pip install --user google-cloud-bigquery
```

Set up the Google Cloud command line tools, in order to set up credentials for connecting to BigQuery. See this link for current release and specific OS: https://cloud.google.com/sdk/docs/install

```bash
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-378.0.0-linux-x86_64.tar.gz

tar zxvf google-cloud-sdk-378.0.0-linux-x86_64.tar.gz

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
export GOOGLE_APPLICATION_CREDENTIALS= /home/ec2-user/dsdemo.json
```

After the `gcloud auth login` command above you would be required to run a provided command on a machine with a web browser and copy its output back here. Make sure the installed gcloud version is 372.0.0 or newer on the other machine with browser.

Install other python packages for the book examples:
```bash
pip install --user matplotlib
pip install --user pyarrow
```