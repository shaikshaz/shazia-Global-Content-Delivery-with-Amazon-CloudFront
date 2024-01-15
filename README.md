# shazia-Global-Content-Delivery-with-Amazon-CloudFront
Global Content Delivery with Amazon CloudFront
Step 1: Create an Amazon S3 Bucket for Static Content
1.	Go to the Amazon S3 Console.
2.	Create a new S3 bucket to host your static website content.
3.	Upload your static content (HTML, CSS, images, etc.) to the S3 bucket.

Give the policy under permission 
4.	{
5.	    "Version": "2012-10-17",
6.	    "Statement": [
7.	        {
8.	            "Sid": "PublicReadGetObject",
9.	            "Effect": "Allow",
10.	            "Principal": "*",
11.	            "Action": "s3:GetObject",
12.	            "Resource": [
13.	                "arn:aws:s3:::shaziabucket2/*",
14.	                "arn:aws:s3:::shaziabucket2"
15.	            ]
16.	        }
17.	    ]
18.	}

Step 2: Configure Amazon CloudFront Distribution for Static Content
1.	Go to the Amazon CloudFront Console.
2.	Click Create Distribution.
3.	In the Origin Settings choose your S3 bucket as the origin.
4.	Configure caching behavior according to your requirements.
5.	Set up additional settings like logging, access control, and tags.
6.	Click Create Distribution.Spin up the DNS of distribution

Step 3: Configure Amazon CloudFront Distribution for Dynamic Content with Lambda@Edge
1.	Go to the AWS Lambda Console.
2.	Create a new Lambda function for dynamic content processing.
3.	Add code to the Lambda function to handle dynamic content generation.
4.	Configure the Lambda function to trigger from the CloudFront distribution.
5.	Add Lambda@Edge triggers for viewer request, origin request, origin response in the dropdown.
Step 4: Configure CloudFront Behaviors for Dynamic and Static Content
1.	In the CloudFront Console, select your distribution.
2.	In the "Behaviors" tab set up behaviors for dynamic and static content.
3.	Configure caching behaviors such as TTL (Time To Live) settings, for optimal performance.
4.	Ensure that Lambda@Edge triggers are correctly configured.
Step 5: Implement Regional Failover with S3 Origins
1.	Create another bucket in other region for regional failover.
2.	Set up failover behaviors for primary bucket by adding in the origin section bucket name and secondary origins.Upload your static website content (HTML, CSS, JS, etc.) to an Amazon S3 bucket.
Configure CloudFront Distribution:
Create a CloudFront distribution and configure it to use the S3 bucket as the origin.
Enable Regional Failover:
Set up a second S3 bucket in another AWS region to serve as a backup.
Configure CloudFront to use the primary S3 bucket as the default origin and the secondary S3 bucket as a failover origin.
Configure DNS for Failover:
Use Amazon Route 53 or another DNS service to set up failover routing. Configure DNS records to point to the CloudFront distribution, and set up health checks to determine when to failover to the secondary S3 bucket.
Step 6: Enable HTTPS for Secure Content Delivery
1.	In the CloudFront Console, select your distribution.
2.	Go to the "General" tab and edit the distribution.
3.	Under "SSL Certificate," choose a custom SSL certificate or use the default CloudFront certificate.
4.	Set the "Viewer Protocol Policy" to "Redirect HTTP to HTTPS" for secure connections.
Step 7: Test and Monitor
1.	Test your CloudFront distribution by accessing your website through the CloudFront domain name.
2.	Monitor the CloudFront and Lambda@Edge metrics in the AWS CloudWatch Console.
3.	Review CloudFront access logs and Lambda@Edge logs for troubleshooting and optimization.
