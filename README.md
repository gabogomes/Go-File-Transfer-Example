# How to Use

This repository was created as part of the Dev Full Cycle course on Golang
specialization. The repository simulates a process of uploading multiple files
in parallel, to an AWS S3 bucket. I used AWS Cloud Guru Playground to simulate
the transference of files to the S3 bucket. To follow the example and check out
in your local environment, follow the steps below (assuming you already started
an AWS Cloud Guru AWS Playground environment):

Use the Access Key ID and Secret Access Key provide by the ACG Platform, and then
export them through your Terminal with the following commands:

```bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...
```

Now you need to generate new credentials that should be valid for one hour:

```bash
aws sts get-session-token --duration-seconds 3600
```

Use the new Access Key ID, Secret Access Key and Session Token to fill in the
parts of `cmd/uploader/main.go` that need to be completed, inside the `init`
function. Also create an S3 bucket in your Playground AWS Account and substitute
the Bucket name in the `s3Bucket` line of the `init` function. Now you have the
code properly configured to handle the upload in your given account and the created
bucket.

Firstly, execute the code to generate 30000 empty files to simulate the parallel upload.
Install all the necessary packages using `go mod tidy`, then use `go run cmd/generator/main.go`.
You should now have a folder called `tmp` and 30000 files inside it.

The next step is to upload all the files to the S3 bucket. Use `go run cmd/uploader/main.go`, which
should handle all the files upload process. Notice that the code also contains logic to perform
retries of failed upload cases. To verify that all the 30000 files successfully made it to the
S3 bucket, use `aws s3 ls s3://bucket-name --recursive --summarize | grep "Total Objects"`. Don't
forget to substitute `bucket-name` by the name of the bucket that you created. The results should be
something like `Total Objects: 30000` printed in the Terminal.