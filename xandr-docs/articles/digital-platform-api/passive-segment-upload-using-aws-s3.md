---
Title : Passive Segment Upload Using AWS S3
Description : If your Xandr member account is integrated with
AWS S3, you can upload segment data into an AWS S3 bucket instead of
actively running API commands against the Batch Segment Service. To set
---


# Passive Segment Upload Using AWS S3



If your Xandr member account is integrated with
AWS S3, you can upload segment data into an AWS S3 bucket instead of
actively running API commands against the Batch Segment Service. To set
up this integration, contact your account support or file an issue at
<a href="http://help.xandr.com/" class="xref"
target="_blank">help.xandr.com</a>. Xandr will
provide upload credentials on initial setup.

After your member is integrated, the Batch Segment Service scans the
`/submitted` directory every five minutes for new data and creates
linkages between users and segments according to the information in your
data files. You can track upload success using the AWS CLI tool at
<a href="https://aws.amazon.com/cli/" class="xref"
target="_blank">https://aws.amazon.com/cli/</a>, using the following
command to display the directory contents:

`AWS_ACCESS_KEY_ID=insert_your_access_key_id_received_from_xandr AWS_SECRET_ACCESS_KEY=insert_your_secret_access_key_id_received_from_xandr aws s3 ls s3://bss-insert_your_member_id-eu-north-1/`

Completed jobs will result in the data file being moved to the `/done`
or `/failed` subdirectory, with a `-JOB_ID` suffix added to the file
name. You can use this information for tracking purposes using the Batch
Segment Service API.

<div id="buy-side-service-template__note_vqr_1pd_vwb"


Note:

Current AWS regions configured for S3 buckets are:

- us-east-2
- us-west-2
- eu-north-1
- eu-west-1

When creating bucket(s) for client, create it/them under us-east-2 by
default, unless specified by client.

If requested, create the bucket under the corresponding region where we
have configured buckets for data uploading.

If requested, create the bucket under the corresponding region where we
have configured buckets for data uploading; **1 bucket is allowed per
region.**



<div id="buy-side-service-template__section_xnt_nzr_zxb"
>

## FAQs



1.  **I have access to the AWS S3 bucket. How can I view the contents of
    the `/submitted` directory?**

    To access the `/submitted` directory, you must create it. Ensure
    that there are no spaces between the forward slash (**/**) and the
    text characters while creating the directory.

2.  **Should I create the `/done` or `/failed` subdirectories?**

    No. The `/done` or `/failed` subdirectories are automatically
    created.

3.  **I have received my AWS S3 login credentials, but I am experiencing
    difficulties logging in.**

    To maintain security, the initial `AWS_ACCESS_KEY_ID` and
    `AWS_SECRET_ACCESS_KEY` login credentials sent to you may be missing
    some characters. For security purposes, we send your credentials in
    two separate communications. Ensure that you have received the
    complete text string of your login from your
    Xandr contact.

4.  **If I don't log in to AWS S3 frequently, will my credentials
    expire?**

    No. Your `access key id` and `secret access key` for AWS S3 does not
    expire.








