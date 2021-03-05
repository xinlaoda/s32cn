# s32cn
s32cn is a bash tools to copy a spcificed amazon s3 bucket or bucket/prefix to China S3, and bassed s3cmd.

The usage is 
s32cn s3://{bucket}/{prefix}/

In this bash scripts, before use, you need edit it and modify following configuration variables:

## Configure
```
_source_cfg=/home/ec2-user/.s3cfg-us
_target_cfg=/home/ec2-user/.s3cfg
_target_bucket="sentinel-s2-l2a-xxin"
_temp_download_root_dir=/home/ec2-user/sentinel-2_data
```
## Installation
1. Install s3cmd
   ```
    sudo yum install python-pip
    sudo pip install s3cmd
   ```
2. Configure s3cmd, include 2 config, one for source, the other for China
   1. Config Global account.
      1. Run command following command
        ```
          s3cmd --configure
        ```
      2. Following the commond, input relate information, complete config
      3. Rename this config file to another name, e.g.
        ```
            mv .s3cfg .s3cfg-us
        ```
        4. Please note if you want to download open-data with requester_pays mode, you need modify variable requester_pays = True
   2. Config China account.
      1. Run command following command
        ```
            s3cmd --configure
        ```
      2. Following the commond, input relate information, complete config, Please note China region has different end-point, e.g. China NingXia region:
        ```
            host_base = s3.cn-northwest-1.amazonaws.com.cn
            host_bucket = %(bucket)s.s3.cn-northwest-1.amazonaws.com.cn
        ```
   
3. Download this scripts from github
   ```
    git clone https://github.com/xinlaoda/s32cn.git
   ```
4. Modify variables in this scripts, for example:
   ```
    _source_cfg=/home/ec2-user/.s3cfg-us
    _target_cfg=/home/ec2-user/.s3cfg
    _target_bucket="sentinel-s2-l2a-xxin"
    _temp_download_root_dir=/home/ec2-user/sentinel-2_data
   ```
   - _target_bucket is s3 bucket name in China region, you need create it in advance.
   - _temp_download_root_dir is the directory full path name in this host to save downloaded data from source s3, you need keep in eye for data volume size.
5. Execute this scripts to copy Global s3 to China s3, for example:
   ```
   ./s32cn s3://sentinel-s2-l2a/tiles/49/S/BU/2021/2/17/0/
   ```
   then, it will download from source backet, and then upload this data into China s3 bucket, and keep the same directory structure.