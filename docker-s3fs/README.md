# S3FS Fuse Docker image

Docker image for [s3fs fuse](https://github.com/s3fs-fuse/s3fs-fuse).

## Configuration

- `AWS_ACCESS_KEY_ID` - (required)
- `AWS_SECRET_ACCESS_KEY` - (required)
- `AWS_STORAGE_BUCKET_NAME` - (required)
- `AWS_S3_AUTHFILE` - path to s3fs auth file.
- `AWS_S3_MOUNTPOINT` - mountpoint default `/mnt`
- `AWS_S3_URL` - s3 endpoint default `https://s3.amazonaws.com`
- `S3FS_ARGS` - additional s3fs mount arguments
- `DEBUG` - enable DEBUG mode.

## Usage example

```bash
docker run --rm -t -i --privileged \
  -e AWS_ACCESS_KEY_ID=AKIAI6ITV3SKKX44NTAQ \
  -e AWS_SECRET_ACCESS_KEY=4G4xbSQOd1OBolDx636MFBLxEwx8gyrxqnoUhRU9 \
  -e AWS_STORAGE_BUCKET_NAME=dev-kegmil-file-storage \
  truyet/docker-s3fs ls /mnt
```

NB, requires `privileged` mode for access to fuse device.

## Status

Stable in production.
