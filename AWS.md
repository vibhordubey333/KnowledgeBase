1. Configuring profile.
   -  `vim ~/.aws/credentials`
       ```
        <profile_name_dev>
        aws_access_key_id = <access_key>
        aws_secret_access_key = <acces_key_secret>

        <profile_name_prod>
        aws_access_key_id = <access_key>
        aws_secret_access_key = <acces_key_secret>

        <profile_name_qa>
        aws_access_key_id = <access_key>
        aws_secret_access_key = <acces_key_secret>
       ```
2. To configure CLI `aws configure`
       
3. `aws s3 ls --profile <profile_name>`

