# rclone-cronjob

A Kubernetes cronjob to sync two object stores using [rclone](http://rclone.org).

- Only supports S3, but may work with other object stores

## How to use

Ensure you are able to use [kustomize](https://kubectl.docs.kubernetes.io/installation/kustomize/) as this will simplify deployment.

1. Rename or duplicate the `overlays/pair-1` directory
1. `kustomization.yaml`
    - Update the `nameSuffix` with your pair number or reference
1. `rclone-secret.env`
    - Update the `rclone-secret.env` file with the credentials for both object stores
1. `rclone.properties`
    - Update the `rclone.properties` file with your rclone config

### Optional

1. `transformer-history-limits.yaml`
    - Update `successfulJobsHistoryLimit` and `failedJobsHistoryLimit` with your preferred job history limits
1. `transformer-schedule.yaml`
    - Update `schedule` with your preferred schedule, for example: `"0 0 * * *"` will cause it to run once a day at midnight

Then run `kubectl apply -k overlays/pair-1`

## How to clean up

Run `kubectl delete -k overlays/pair-1`
