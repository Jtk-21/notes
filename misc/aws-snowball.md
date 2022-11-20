# AWS Snowball

Configure IP of Snowball on Device

Install `awsclibunddle` and `snowballclient`

Unlock Snowball using `snowballclient`
`snowballedge.bat unlock -i <snowball_IP> -m <manifest_file> -u <unlock_code>`

Get Status
`snowballedge.bat status -i <snowball_IP> -m <manifest_file> -u <unlock_code>`

Credentials
`snowballedge.bat credentials -i <snowball_IP> -m <manifest_file> -u <unlock_code>`
This will provide the `aws_access_key_id` and `aws_secret_key` used in the aws client

Run `awsconfigure` and input keys from previous step

Copy from Local to Snowball
`aws s3 cp <local_file> s3://<path> --endpoint http://<snowball_IP>:8080`

`aws s3 cp --recursive`

Directory Listing
`aws s3 ls s3://<path> --endpoint http://<snowball_IP>:8080`

Remove File
`aws s3 rm`





