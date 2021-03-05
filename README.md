# s32cn
s32cn is a bash tools to copy a gived amazon s3 bucket or bucket/prefix to China S3.

The usage is 
s32cn s3://{bucket}/{prefix}

In this bash scripts, before use, you need edit it and modify following configuration variables:

# configure
_source_cfg=/home/ec2-user/.s3cfg-us
_target_cfg=/home/ec2-user/.s3cfg
_target_bucket="sentinel-s2-l2a-xxin"
_temp_download_root_dir=/home/ec2-user/sentinel-2_data
