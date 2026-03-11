# s3simple

s3simple is a small bash script/function for fetching objects from and putting
files into Amazon’s S3 Simple Storage service.

It is intended for use in early bootstrapping of a system, and it has only two
dependencies (curl and openssl), both of which are usually pre-installed or
easily available as packages. If the [AWS CLI][] is available you should use it
instead of this script.

[AWS CLI]: https://aws.amazon.com/cli/

## Usage

1. Download the [s3simple](s3simple) script somewhere.
2. Set `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` and optionally
`AWS_SESSION_TOKEN` environment variables. Set `AWS_DEFAULT_REGION` or
`AWS_REGION` to specify your region (defaults to `us-east-1`). To use an
S3-compatible endpoint (e.g. MinIO, Ceph, Backblaze B2), set `S3_ENDPOINT_URL`.
3. Run `s3simple` with a method, an `s3://` url and, optionally, a local
filename.

For example:

    export AWS_ACCESS_KEY_ID=AKxxx
    export AWS_SECRET_ACCESS_KEY=zzzz
    # optionally provide a temporary session token
    export AWS_SESSION_TOKEN=wwww...

    # list objects in a bucket
    ./s3simple ls s3://mybucket

    # list objects with a prefix
    ./s3simple ls s3://mybucket/path/prefix

    # get a file
    ./s3simple get s3://mybucket/myfile.txt myfile.txt

    # fetch metadata about an object
    ./s3simple head s3://mybucket/myfile.txt

    # put a file
    ./s3simple put s3://mybucket/foo.txt foo.txt

    # get a file and pipe to tar
    s3simple get s3://mybucket/foo.tgz | tar -zx

    # use a custom S3-compatible endpoint
    export S3_ENDPOINT_URL=https://minio.local:9000
    ./s3simple get s3://mybucket/myfile.txt myfile.txt

You are encouraged to copy the s3simple function into your bash scripts and edit
it to suit your needs.

## License

MIT license, see LICENSE.txt for details.
