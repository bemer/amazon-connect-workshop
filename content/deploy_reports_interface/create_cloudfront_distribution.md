+++
title = "Create a CloudFront distribution"
weight = 52
+++

In order to serve the content of your newly deployed website, you can be leveraging the S3 bucket static website hosting feature, but a best practice is that you leverage a CloudFront distribution instead. This is going to help you to speed up the delivery of the assets as well as save with data transfer out costs.

To do so, acces the [CloudFront console](https://console.aws.amazon.com/cloudfront/home). In the CloudFront screen, click in the **Create Distribution** button.

![CloudFrontCreateDistribution](/images/deploy-reports-interface/create_distribution.png)

After clicking on the Create Distribution button, click in **Get Started** on the next screen. You will see the distribution configuration page. The first think you have to do is to select the bucket provisioned by the CloudFormation template in the **Origin Domain Name** section:

![SelectS3Bucket](/images/deploy-reports-interface/select_bucket.png)

After selecting the bucket, make sure you change the following options:

- **Restrict Bucket Access: Yes**
- **Origin Access Identity: Create a New Identity**
- **Grant Read Permissions on Bucket: Yes, Update Bucket Policy**

![OriginConfiguration](/images/deploy-reports-interface/origin_configuration.png)

After changing the Origin Settings, chante the **Viewer Protocol Policy** to **Redirect HTTP to HTTPS**.

After changing these fields, click in **Create Distribution** button.

It will take a few minutes until your distribution is fuly deployed. When it finishes, you will see the status as **Deployed** on the [Amazon CloudFront console](https://console.aws.amazon.com/cloudfront/home).

When the CloudFront distribution deployment is complete, you will be able to get the access URL under the **Domain Name** field. Copy this domain name and access it with your browser by adding **/metrics/metrics.html** to the path:

![DistributionFrontUrl](/images/deploy-reports-interface/cloudfront_distribution_url.png)

In my case, the URL will be **davwvknx9ps1s.cloudfront.net/metrics/metrics.html**. When acessing it, I'll be able to see the reporting interface. 

![ApplicationInterface](/images/deploy-reports-interface/app_interface.png)


This means that the initial deployment worked fine and we can move to the addition setup pieces.