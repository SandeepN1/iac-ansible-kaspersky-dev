Role Name
=========

The ansible role `Kaspersky` is used to install and configure the Kaspersky Agent on Windows

Version & Author
----------------

```

VER | [ MM/DD/YYYY] | COMMENTS [AUTHOR]

1.0 | [11/01/2022] | Create Kaspersky install role for Windows [ Aman Kumar ]
                   | Update variable Structure to Include Onprem and Cloud [ Ravi Singh ]
      [13/01/2022] | Update README and CHANGELOG [ Ravi Singh ]

```

Requirements
------------

### OS Supported

* Windows

### Requirements

* Kaspersky package available in your OS software repository or stored in an ***AWS*** S3 bucket
* For Windows WINRM should be enabled
* Vault password should be known

Role Variables
--------------
| Variable | Type | Description | Required |
| ---  | ---  | ---  | --- |
| kaspersky_pkg | string | Kaspersky package version to install. For S3 download use the full package name stored in S3. | true |
| kaspersky_s3_bucket | string   | Set ONLY if you are using an S3 bucket to store Kaspersky install package. | true  |
| kaspersky_s3_bucket_win_folder | string | Folder under S3 where kaspersky binary is stored . | true |
| kaspersky_pkg_windows | string | Package name for Windows binary install | true |


Dependencies
------------

* Botocore,AWSCLI and Boto3 must be installed
* For Windows Python ,AWSCLI and Boto3 must be installed
* For Windows WINRM should be enabled .

Example Playbook When Using OS Native Package Manager
----------------
```
- hosts: all
  roles:
    - role: kaspersky
```

Example when downloading install from S3 bucket

```
- hosts: all
  roles:
    - role: kaspersky
        kaspersky_s3_bucket: "ma_bucket"

ansible-playbook -i hosts kaspersky.yml -u root -e "kaspersky_s3_bucket=xxxxxxxxx"  --vault-password-file <location of vault password>
ansible-playbook -i hosts kaspersky.yml -u root --vault-password-file /var/tmp/test
```

Example Windows

```
hosts

[all]
34.241.68.25
34.245.45.252

ansible-windows ansible_connection=winrm ansible_host=35.232.181.229 ansible_password='xxxxxxxxxxxx' ansible_user=admin ansible_winrm_server_cert_validation=ignore

eg
ansible-playbook kaspersky.yml -i hosts --limit ansible-windows --vault-password-file /var/tmp/test
ansible-playbook -i hosts kaspersky.yml --vault-password-file /var/tmp/test
```


Support Information
-------------------


MAF Orchestration and Automation
| Support                                      | Team                                                                                                                                      |
| ---------------------| -------------------------------------------- |
| App Code:                              |MAF IAC
| DL:                  |
| GIT Project:         |
