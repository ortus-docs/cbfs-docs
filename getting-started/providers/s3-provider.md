---
description: Leverage the s3 provider to store files in an s3 compatible file-system.
---

# S3 Provider

Use the S3 provider to store files within any S3 compatible file storage service such as AWS S3 or Digital Ocean Spaces.

{% hint style="success" %}
The S3 provider uses the [s3sdk](https://forgebox.io/view/s3sdk) library for all s3 operations.
{% endhint %}

{% hint style="warning" %}
Keep in mind when using this provider that all file operations result in an outgoing network request from your application. We have utilized various caching techniques to ensure fast operations, but it's good to be mindful of these outgoing requests when working with files and folders.
{% endhint %}

## Configuration

### Example

{% code title="config/ColdBox.cfc" %}
```json
moduleSettings = {
	"cbfs": {
		// The default disk with a reserved name of 'default'
		"defaultDisk" : "myStorage",
		// Register the disks on the system
		"disks"       : {
			// Your default application storage
			"myStorage" : {
				"provider": "S3",
				"properties": {
					"visibility": "public", // can be 'public' or 'private'
					"path": "",
					"accessKey": "",
					"secretKey": "",
					"awsDomain": "digitaloceanspaces.com",
					"awsRegion": "sfo3",
					"defaultBucketName": "myDOSpace"
				}
			}
		}
	},
};
```
{% endcode %}

### Properties

This provider uses the [s3sdk](https://forgebox.io/view/s3sdk) library under the hood, and any of the properties that can be passed in are available, most of which are documented here.&#x20;

| Property              | Type    | Default                             | Description                                                                                             |
| --------------------- | ------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `autoContentType`     | boolean | `false`                             |                                                                                                         |
| `autoMD5`             | boolean | `false`                             |                                                                                                         |
| `accessKey`           | string  | --                                  | Your S3 access key                                                                                      |
| `awsDomain`           | string  | --                                  | The domain name used to connect to your s3 service provider                                             |
| `awsRegion`           | string  | --                                  | The region name used to connect to your s3 service provider                                             |
| `cacheLookups`        | boolean | `true`                              |                                                                                                         |
| `debug`               | boolean | `false`                             |                                                                                                         |
| `defaultTimeout`      | numeric | 300                                 | The default timeout of the http operations                                                              |
| `defaultDelimiter`    | string  | `/`                                 | Default delimiter to use                                                                                |
| `defaultBucketName`   | string  | --                                  | The bucket name, within which this disk operates.                                                       |
| `defaultCacheControl` | string  | no-store, no-cache, must-revalidate |                                                                                                         |
| `defaultStorageClass` | string  | `STANDARD`                          |                                                                                                         |
| `secretKey`           | string  | --                                  | Your S3 secret key                                                                                      |
| `defaultACL`          | string  | `public-read`                       |                                                                                                         |
| `encryptionCharset`   | string  | `UTF-8`                             | The encoding characterset                                                                               |
| `publicDomain`        | string  | --                                  | Will be the public domain in URLs generated - for example, when using a CDN distribution via CloudFront |
| `retriesOnError`      | numeric | `3`                                 |                                                                                                         |
| `serviceName`         | string  | `s3`                                |                                                                                                         |
| `signatureType`       | string  | `v4`                                | Which signature encoding to use, `v4` is the latest.                                                    |
| `ssl`                 | boolean | `true`                              | Use SSL for all operations                                                                              |
| `throwOnRequestError` | boolean | `true`                              |                                                                                                         |
| `uploadMimeAccept`    | string  | \*                                  | The mime types which are accepted via the upload method. Defaults to all.                               |
| `visibility`          | string  | public                              | Whether the contents of the disk are public (world read ) or private                                    |

### Bucket Configuration Considerations

File operations, including the setting of permissions on objects within an AWS bucket require both configuration settings to the bucket and to the user account, in order to all CBFS operations.

#### User Permissions

In the IAM section of the AWS Manager, your user account should, at minimum have an ACL policy that grants them access to all S3 operations on the bucket.  Below is an example of a JSON IAM policy which grants an AWS user access to all bucket operations - including encryption and decryption if that feature is enabled on the bucket:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1412062044000",
            "Effect": "Allow",
            "Action": [
                "s3:*",
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:GenerateDataKey"
            ],
            "Resource": [
                "arn:aws:s3:::my-bucket-name",
                "arn:aws:s3:::my-bucket-name/*"
            ]
        }
    ]
}
```

#### Bucket Permissions

When creating a bucket to be used with CBFS operations, some initial settings need to be configured, in order for the user you created to perform permissions operations on objects within the bucket.  For a non-root user account to perform operations, the following changes to the default configuration must be performed:

1.  Enable ACL's in the **Permissions > Object Ownership**\
    ****\
    ****

    <figure><img src="../../.gitbook/assets/AWS-Bucket-Ownership-Settings.jpg" alt=""><figcaption></figcaption></figure>
2.  Edit **Permissions > Block Public Access** to allow the IAM users to set their own permissions on objects created. If your bucket is private this will allow the explicit settings for those objects to be peformed.\
    \


    <figure><img src="../../.gitbook/assets/AWS-Public-Access-Settings.jpg" alt=""><figcaption></figcaption></figure>

Note that we have disabled the inheritance settings above, which allows new ACL policies to be created on object, but still disables any cross-account ACL settings, for security.

For public buckets, it is also recommended that you complete the Permissions > CORS section to allow access to your objects only from specific domain referrers.
