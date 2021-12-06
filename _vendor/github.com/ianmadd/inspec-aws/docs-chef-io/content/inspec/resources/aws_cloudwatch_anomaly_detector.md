+++
title = "aws_cloudwatch_anomaly_detector Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_cloudwatch_anomaly_detector"
identifier = "inspec/resources/aws/aws_cloudwatch_anomaly_detector Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Migration Links for Review</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_cloudwatch_anomaly_detector.md">https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_cloudwatch_anomaly_detector.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_cloudwatch_anomaly_detector.md">https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_cloudwatch_anomaly_detector.md</a></p>
</div>
</div>


Use the `aws_cloudwatch_anomaly_detector` InSpec audit resource to test properties of a single specific AWS CloudWatch anomaly detector.

The `AWS::CloudWatch::AnomalyDetector` type specifies an anomaly detection band for a certain metric and statistic. The band represents the expected "normal" range for the metric values. Anomaly detection bands can be used for visualization of a metric's expected values, and for alarms.

For additional information, including details on parameters and properties, see the [AWS documentation on AWS CloudWatch AnomalyDetector.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudwatch-anomalydetector.html).

## Installation

{{% inspec_aws_install %}}

## Syntax

Ensure that the anomaly detector exists.

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
  it { should exist }
end
```

## Parameters

`metric_name` _(required)_

: The name of the metric associated with the anomaly detection model.

## Properties

`namespace`
: The namespace of the metric associated with the anomaly detection model.

`metric_name`
: The name of the metric associated with the anomaly detection model.

`dimensions`
: The metric dimensions associated with the anomaly detection model.

`dimensions_names`
: The name of the dimension.

`dimensions_values`
: The value of the dimension.

`stat`
: The statistic associated with the anomaly detection model.

`configuration_start_time`
: The start time of the range to exclude.

`configuration_end_time`
: The end time of the range to exclude.

`configuration.metric_timezone`
: The time zone to use for the metric.

`state_value`
: he current status of the anomaly detector's training. The possible values are TRAINED, PENDING_TRAINING and TRAINED_INSUFFICIENT_DATA.

## Examples

**Ensure a namespace is available.**

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
  its('namespace') { should eq 'NAMESPACE' }
end
```

**Ensure a config name is available.**

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
    its('name') { should eq 'CONFIG_NAME' }
end
```

**Ensure a dimension name is available.**

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
    its('dimensions_names') { should include 'DIMENSION_NAME' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

The controls will pass if the `describe` method returns at least one result.

### exist

Use `should` to test that the entity exists.

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
  it { should exist }
end
```

Use `should_not` to test the entity does not exist.

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
  it { should_not exist }
end
```

### be_available

Use `should` to check if the entity is available.

```ruby
describe aws_cloudwatch_anomaly_detector(metric_name: 'METRIC_NAME') do
  it { should be_available }
end
```

## AWS Permissions

{{% aws_permissions_principal action="CloudWatch:Client:DescribeAnomalyDetectorsOutput" %}}
