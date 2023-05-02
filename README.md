Hatching Triage
===============

This repository features a command-line client and API for interacting with
[Hatching Triage](https://tria.ge/), an automated malware analysis sandbox.

Our official command-line and API client is implemented in both Golang as
well as Python. For a Java library, please see
[TriageApi by Libra](https://github.com/ThisIsLibra/TriageApi).

## Getting Started

### Installing the Go client

```bash
$ go get github.com/hatching/triage/go/cmd/triage
```

### Installing the Python client

```bash
$ pip install hatching-triage
```

## Setting up authentication

When you have installed the client, you need to set the API key so it can
authenticate itself with Triage. You can do so by using the `authenticate`
subcommand:

```bash
$ triage authenticate <API key>
```

You can find the API key on your [account page](https://tria.ge/account). Do
note that you need to have a Researcher account on your user account for a key
to appear.

## Usage

After installing and authentication, various subcommands are available for
interacting with the Hatching Triage API. Note that any submitted samples will
end up in our public cloud, unless otherwise configured, and therefore will
be accessible by everyone browsing to https://tria.ge/

```bash
$ triage -help
Usage of triage:

  authenticate [token] [flags]

    Stores credentials for Triage.

  submit [url/file] [flags]

    Submit a new sample file or URL.

  select-profile [sample]

    Interactively lets you select profiles for samples that have been submitted
    in interactive mode. If an archive file was submitted, you will also be
    prompted to select the files to analyze from the archive.

  list [flags]

    Show the latest samples that have been submitted.

  file [sample] [task] [file] [flags]

    Download task related files.

  archive [sample] [flags]

    Download all task related files as an archive.

  delete [sample]

    Delete a sample.

  report [sample] [flags]

    Query reports for a (finished) analysis.

  create-profile [flags]

  delete-profile [flags]

  list-profiles [flags]
```


## Usage - triage.Client

### \_\_init__
`token`: String

`root_url:` String
* default: https://api.tria.ge


### submit_sample_file
`filename`: String

`file`: File

`interactive`: Boolean
* default: False

`profiles`: String[]
* default: []

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#submitting-a-file


### submit_sample_url
`url`: String

`interactive`: Boolean
* default: False

`profiles`: String[]
* default: []

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#submitting-a-url

### set_sample_profile
`sample_id`: String

`profiles`: String[]


##### Return JSON
{}

### set_sample_profile_automatically
`sample_id`: String

`pick`: String[]
* default: []

##### Return JSON
{}

### owned_samples

`max`: Int
* default: 20

##### Return Paginator
https://tria.ge/docs/cloud-api/samples/#get-samples

### public_samples

`max`: Int
* default: 20

##### Return Paginator
https://tria.ge/docs/cloud-api/samples/#get-samples

### search_samples

`query`: String
`max`: Int
* default: 20

##### Return Paginator
https://tria.ge/docs/cloud-api/samples/#get-samples

### sample_by_id

`sample_id`: String

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#get-samplessampleid

### delete_sample

`sample_id`: String

##### Return JSON
{}

### static_report

`sample_id`: String

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#get-samplessampleidreportsstatic

### overview_report

`sample_id`: String

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#get-samplessampleidoverviewjson

### task_report

`sample_id`: String

`task_id`: String

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#get-samplessampleidtaskidreport_triagejson


### sample_task_file

`sample_id`: String

`task_id`: String

`filename`: String

##### Return binary data
file contents

### sample_archive_tar

`sample_id`: String

##### Return binary data
file contents

### sample_archive_zip

`sample_id`: String

##### Return binary data
file contents

### create_profile

`name`: String

`tags`: String[]

`network`: String[]
* Either \"internet\", \"drop\" or None

`timeout`: Int

##### Return JSON
https://tria.ge/docs/cloud-api/profiles/

### delete_profile

`profile_id`: String

##### Return JSON
{}

### profiles

##### Return Paginator
https://tria.ge/docs/cloud-api/profiles/


### sample_events

`sample_id`: String

##### Return JSON
https://tria.ge/docs/cloud-api/samples/#get-samplesevents
