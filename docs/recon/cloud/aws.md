---
title: AWS
parent: Cloud
nav_order: 1
---

Mainly using `awscli` to access
Install awscli first, then type `aws configure` to configure new account. Type in your AWS access key ID (AKIAGGGGGGGGGGGGG) and secret access key: (osUw5ZXqwKZhhCZ9Yg0DkLokI+iusP6HJziA9wBx). Leave the rest to default.
After configuring, try to ls the s3 bucket (usually will be the same as the http website. If the domain containing the file is https://assets.example.com, can try s3://assets.example.com).\
Can do this by the command below:\
`aws s3 ls s3://assets.example.com`\
You can also ls a file directly by using:\
`aws s3 ls s3://assets.example.com/exampletxt.txt`\
If ls don't work, can try copying the file:\
`aws s3 cp s3://assets.example.com/exampletxt.txt example.txt`
