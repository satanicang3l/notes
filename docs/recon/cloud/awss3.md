---
title: AWS S3
parent: Cloud
nav_order: 2
---

Can just try to use aws configure and put in random values because sometimes server won't check authentication.

To list buckets, use\
`aws --endpoint=http://s3.domain s3 ls`. 

To list all objects and prefixes for the buckets, use\
`aws --endpoint=http://s3.domain s3 ls s3://bucketname`. 

To download/upload the file (can upload shell if front end visible), use\
`aws --endpoint=http://s3.domain s3 cp s3://bucketname/filename filenametobesavedtolocal` or vice versa if want to upload.