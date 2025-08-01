# MinIO

MinIO is a High-Performance Object Storage released under GNU Affero General Public License v3.0. It is API compatible with the Amazon S3 cloud storage service. It is capable of working with unstructured data such as photos, videos, log files, backups, and container images with the maximum supported object size being 50TB.

wikipedia.org/wiki/MinIO

<img src="https://min.io/resources/img/logo/MINIO_wordmark.png" width="80%" height="auto">

## How to use this Makejail

```
mkdir -p .volumes/minio-data
appjail makejail \
    -j minio \
    -f gh+AppJail-makejails/minio \
    -o virtualnet=":<random> default" \
    -o nat \
    -o expose=9000 \
    -o expose=9001 \
    -o fstab="$PWD/.volumes/minio-data minio-data <volumefs>"
appjail start \
    -V MINIO_ROOT_USER="AKIAIOSFODNN7EXAMPLE" \
    -V MINIO_ROOT_PASSWORD="wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" \
    minio
```

### Arguments (stage: build):

* `minio_tag` (default: `13.5`): See [#tags](#tags).
* `minio_ajspec` (default: `gh+AppJail-makejails/minio`): Entry point where the `appjail-ajspec(5)` file is located.

### Check current status

The custom stage `minio_status` can be used to run `top(1)` to check the status of Flatnotes.

```sh
appjail run -s minio_status minio
```

### Log

To view the log generated by the web application, run the custom stage `minio_log`.

```sh
appjail run -s minio_log minio
```

### Environment (stage: start)

* `MINIO_ARGS` (optional): MinIO arguments.

### Volumes

| Name       | Owner | Group | Perm | Type | Mountpoint    |
| ---------- | ----- | ----- | ---- | ---- | ------------- |
| minio-data | 473   | 473   |  -   |  -   | /var/db/minio |

## Tags

| Tag    | Arch    | Version        | Type   |
| ------ | ------- | -------------- | ------ |
| `13.5` | `amd64` | `13.5-RELEASE` | `thin` |
| `14.3` | `amd64` | `14.3-RELEASE` | `thin` |
