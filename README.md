# rclone-cronjob

A Kubernetes cronjob to sync two object stores using [rclone](http://rclone.org).

- Only supports S3, but may work with other object stores
- Runs every 5 minutes

## How to use

Update the `configmap.yaml` with your rclone config, for example:

```yaml
  RCLONE_OPTS: "--fast-list"
  RCLONE_LOG_LEVEL: INFO # DEBUG, INFO, WARNING, ERROR
  RCLONE_METHOD: sync # or copy
  # Source and destination config
  SOURCE_TYPE: s3
  SOURCE_PROVIDER: AWS
  SOURCE_BUCKET: my-first-bucket
  SOURCE_ENDPOINT: s3-accesspoint.af-south-1.amazonaws.com
  DESTINATION_TYPE: s3
  DESTINATION_PROVIDER: Linode
  DESTINATION_BUCKET: my-second-bucket
  DESTINATION_ENDPOINT: nl-ams-1.linodeobjects.com
```

Update the `secrets.yaml` with your credentials:

```yaml
  source_access_key: # replace with your source access key
  source_secret_key: # replace with your source secret key
  destination_access_key: # replace with your destination access key
  destination_secret_key: # replace with your destination secret key
```

Then run `kubectl apply -f .`
