---
title: "Quick Start - Hello World"

rightPanel: OFF


---
# Getting Started

You can access Dow Jones content via a wide range of tools, including APIs (REST 1, REST 2, and SOAP), and XML feeds via FTP. Depending on the content you need to access, you can perform the authentication process with a single API key in the request headers, or using the OAuth 2.0 authentication method. You will receive an email containing your relevant credentials from the Dow Jones Developer Support team.

## Hello World: Factiva Snapshots

The following is an example query object. Learn more about searching and filtering in API Essentials.

```
request_body = {
  "query": {
    "where": "language_code='en'",
    "includes": {
      "company_codes": ["exxn"] # only documents that contain company_code "exxn" will be returned
    },
    "limit": 10000
  }
}
```

Use your API Key to authenticate to Factiva Snapshots. The following is an example of the `headers` object required for authentication:

```
headers = {
    'content-type': 'application/json', 
    'user-key': '{USER_KEY}'
}
```

The Snapshots API works asynchronously. First, you make a Post request to the Snapshots URL endpoint as follows:

```
snapshot_url = "https://api.dowjones.com/alpha/extractions/documents"

requests.post(snapshot_url, data=json.dumps(request_body), headers=headers)
```

If successful, this request generates a snapshot creation job. The following is an example response:

```
{
  "data": {
    "attributes": {
      "current_state": "JOB_QUEUED",
      "extraction_type": "documents"
    },
    "id": "dj-synhub-extraction-mixoflettersandnumber1234567890"
  },
  "links": {
    "self": "https://api.dowjones.com/alpha/extractions/documents/dj-synhub-extraction-sample-extraction"
  }
}
```

You can use Get requests sent to the URL in `response.links.self` to monitor the status of your snapshot, as follows:

```
requests.get(self_link, headers=headers)
```

Once the snapshot is complete, `response.data.attributes.current_state` displays the message `JOB_STATE_DONE`. You then get a new key called `files`, which contains the file download links, as follows:

```
{
  "data": {
    "attributes": {
      "current_state": "JOB_STATE_DONE",
      "files": [
        {
          "uri": "https://api.dowjones.com/alpha/extractions/stream?file=dj-syndicationhub-dev-delivery/part-00000-of-0001.avro"
        },
        {
          "uri": "https://api.dowjones.com/alpha/extractions/stream?file=dj-syndicationhub-dev-delivery/format=avro/jwhuvuexzy/part-00001-of-00001.avro"
        }]
    },
    "id": "dj-synhub-extraction-sample-extraction"
  },
  "links": {
    "self": "https://api.dowjones.com/alpha/extractions/dj-synhub-extraction-sample-extraction"
  }
}
```

Access these links directly to download the relevant files.
