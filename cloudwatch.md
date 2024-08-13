
## Step-by-Step Guide to Monitoring Bedrock with CloudWatch

## Step 1: Enabling Model Invocation Logging

To enable logging, access the Bedrock console\'92s Settings page via the left navigation bar. Here, you\'92ll find the option to toggle Model Invocation Logging, prompting you to specify the types of data to be logged, such as text, images, and embeddings.

To configure logging, navigate to the Settings page in the Bedrock console, from the left navigation bar.

[Settings page](https://us-east-1.console.aws.amazon.com/bedrock/home?region=us-east-1#/settings)

![](https://miro.medium.com/v2/resize:fit:1400/1*Ia2aYnLI6BiozzRndPGA6w.png)

Then toggle the Model invocation logging button which will present you with several fields that will need to be filled out before logging can be enabled.

First, select the data types to include with logs. You can choose text, image and embedding.

## Step 2: Selecting a Logging Destination

Next, select your logging destination,

Select your logging destination, where you have three options. The first option is S3 Only which configures Bedrock to only send logs to a S3 bucket of your choice. The second option is CloudWatch Logs only, which sends the logs to CloudWatch and when model input or output data is larger than 100kb or in binary format it can be optionally delivered to S3. The last option is Both S3 & CloudWatch Logs where logs are sent to both S3 & CloudWatch and when model input or output data is larger than 100kb or in binary format data it will only be sent to S3. Whatever option you choose you remain in control of model inputs and outputs, including encryption with KMS and retention duration. In my case I have chosen the CloudWatch Logs only option.

- S3 Only: Directs logs exclusively to an Amazon S3 bucket.

- CloudWatch Logs Only: Sends logs to CloudWatch, with the option to offload larger or binary data to S3.

- Both S3 & CloudWatch Logs: Logs are sent to both destinations, with large or binary data being S3-exclusive.

Each option offers full control over data management, including encryption via KMS and setting data retention durations.

![](https://miro.medium.com/v2/resize:fit:1400/1*XKOwtOAoPUFJRvZZ1udKpw.png)

## Step 3: Configuring CloudWatch Log group and S3 Settings

After choosing your logging destination, create a log group in CloudWatch and an S3 bucket for large data files. Within the Bedrock Settings, link your newly created S3 bucket for large data delivery and finalize the setup by saving your changes.

![](https://miro.medium.com/v2/resize:fit:1400/1*7cQfFcVZsHtdwH5adBItow.png)

## Step 4 : Specifying a CloudWatch Log Group for Model Invocation Logging

After enabling model invocation logging in the Bedrock console, you\'92ll need to specify where these logs should be stored within CloudWatch. This involves:

- Navigating back to the Model Invocation Console within Bedrock.

- Locating the CloudWatch Logs configuration section.

- Specifying a unique log group name.

A log group in CloudWatch is a container that holds a collection of log streams, which in turn contain the actual log events. By specifying a log group name, you are instructing Bedrock to send its logs to a specific place within CloudWatch, where they can be organized, monitored, and accessed easily. This step is crucial for managing logs effectively, as it allows for better organization and retrieval of log data related to model invocations.

![](https://miro.medium.com/v2/resize:fit:1400/1*Uxue6jckz7ienfOOshhTtg.png)

## Step 5 : Creating an S3 Bucket for Log Storage

Amazon S3 (Simple Storage Service) offers scalable object storage. When dealing with large amounts of log data or logs that include large files (such as images or embeddings), it\'92s often necessary to store them in an S3 bucket. This step involves:

- Going to the Amazon S3 console.

- Creating a new bucket, which involves specifying a unique name for the bucket and configuring settings such as region, access permissions, and other options depending on your requirements.

S3 buckets are used in conjunction with CloudWatch Logs when logs are too large or in a format that is better suited for S3 storage. It ensures that all data, regardless of size, is stored securely and efficiently, with the flexibility to access and analyze this data as needed.

![](https://miro.medium.com/v2/resize:fit:1400/1*9AoWuX05VSWGnHf5tT3BKQ.png)

## Step 6: Integrating the S3 Bucket with Bedrock Logging Configuration

After creating an S3 bucket, the next step is to link this bucket with the Bedrock logging configuration. This involves:

- Returning to the Bedrock Settings page.

- Navigate to the section where you previously selected your logging destination.

- Inputting the URL or ARN (Amazon Resource Name) of your newly created S3 bucket into the relevant field, specifically for \'93S3 bucket for large data delivery.\'94

By adding the S3 bucket URL to the Bedrock configuration, you ensure that any log data, especially those exceeding size limits for CloudWatch or in binary format, are automatically sent to the specified S3 bucket. This setup provides a comprehensive logging solution that leverages both CloudWatch for real-time monitoring and analytics, and S3 for durable, scalable storage of large or binary log files.

![](https://miro.medium.com/v2/resize:fit:1400/1*NoeSw50ApUUbk_0N_hhwEQ.png)

Once the model invocation logs are being delivered, you can use two features in CloudWatch to inspect your logs. The first is Live Tail and the second is Log Insights.

## Generating log data from Bedrock

CloudWatch Logs Insights enables you to interactively search and analyze your log data in CloudWatch Logs. You can perform queries to help you more efficiently and effectively respond to operational issues.

In the case of Bedrock we can use Log Insights to search and analyze the model invocation logs and search for specific keywords or simply the latest invocation logs

![](https://miro.medium.com/v2/resize:fit:1400/1*7admtOJDljiTk2lhmP64bg.png)

## Streaming logs using Live Tail

Live Tail in CloudWatch Logs is a feature that provides an interactive log analytics experience that helps you view your logs interactively in near real-time as they\'92re ingested. Live Tail provides customers a rich out-of-the-box experience to view and detect issues in their incoming logs. Additionally, it provides fine-grained controls to filter, highlight attributes of interest, and pause/replay logs while troubleshooting issues

![](https://miro.medium.com/v2/resize:fit:1400/1*2AS5et2h4b1p3jL3qMqfHQ.png)


## Bedrock Runtime Metrics

Bedrock also sends near real-time metrics to CloudWatch, which can be used to set alarms that watch for certain thresholds, and then send notifications or take actions when values exceed those thresholds. You can also enable CloudWatch anomaly detection for metrics which applies statistical and machine learning algorithms that continuously analyze metrics, determine normal baselines, and surface anomalies with minimal user intervention.

[CloudWatch anomaly detection](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Anomaly_Detection.html)

![Visualization showing the number of invocations over a 15-minute period with a stacked area chart with Anthropic Claude v1 and Anthropic Claude v2 metrics in CloudWatch.](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2023/10/10/CloudWatchBedrock-Metrics.png)

Figure 9: Visualization showing the number of invocations over a 15-minute period with a stacked area chart with Anthropic Claude v1 and Anthropic Claude v2 metrics in CloudWatch.

The runtime metrics provided by Bedrock are shown below and can also be found here:

[here](https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-cw.html#runtime-cloudwatch-metrics)

These metrics can be used for a variety of use cases including:

- Comparing latency between different models using the InvocationLatency metric with ModelId dimension

- Measuring token count (input & output) to assist in purchasing provisioned throughput by analyzing the InputTokenCount and OutputTokenCount

- Detecting and alerting on throttling with an CloudWatch Alarm with the InvocationThrottles metric

For simplicity, the logs and metrics that Bedrock sends to CloudWatch can be presented as a single view using CloudWatch dashboards. If you have multiple AWS accounts, you can setup CloudWatch cross-account observability and then create rich cross-account dashboards in your monitoring accounts.

![CloudWatch Dashboard showing the number of invocations over time by model, invocation latency by model, token count by input & output, and latest prompts from model invocation logs.](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2023/10/10/CloudWatchBedrock-Dashboard.jpg)

Figure 10: CloudWatch Dashboard showing the number of invocations over time by model, invocation latency by model, token count by input & output, and latest prompts from model invocation logs.

In dashboard above we are showing the following information:

- The number of invocations over time by model

- Invocation latency by model

- Token count by input and output tokens

- The latest prompts from the invocation logs showing the model, operation, input and output token count.