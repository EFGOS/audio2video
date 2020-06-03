# audio2video

Upload `.mp3` file to S3 Bucket and wait for Lambda to create `.mp4` file into same S3 Bucket. See CloudWatch logs for details and debuging purposes.

Heavily inspired from https://serverless.com/blog/publish-aws-lambda-layers-serverless-framework/

## Prepare ffmpeg layer
```bash
mkdir layer
cd layer
curl -O https://johnvansickle.com/ffmpeg/builds/ffmpeg-git-amd64-static.tar.xz
tar xf ffmpeg-git-amd64-static.tar.xz
rm ffmpeg-git-amd64-static.tar.xz
mv ffmpeg-git-*-amd64-static ffmpeg
cd ..
```

## Deploy
```bash
serverless deploy
```

## Usage

### Upload image/jpg file
```bash
aws s3 cp ./example.jpg s3://${bucket}/images/
```

### Upload audio/mp3 file

```bash
aws s3 cp ./example.mp3 s3://${bucket}/uploads/
```

### Wait for lambda function to complete
```bash
# watch logs
serverless logs --tail --function mkvideo
```

### Download result/mp4 file
```bash
aws s3 cp s3://${bucket}/results/example.mp4 ./
```

## Cleanup

### Empty bucket
```bash
aws s3 rm s3://${bucket} --recursive
```

### Remove deployment
```bash
serverless remove
```