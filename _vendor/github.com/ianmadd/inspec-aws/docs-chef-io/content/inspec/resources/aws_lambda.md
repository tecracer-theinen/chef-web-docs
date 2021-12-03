+++
title = "aws_lambda Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_lambda"
identifier = "inspec/resources/aws/aws_lambda Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_lambda.md">aws_lambda.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_lambda.md">aws_lambda.md</a></p>
</div>
</div>



Use the `aws_lambda` resource to test a specific lambda.

## Installation

{{% inspec_aws_install %}}

## Syntax

````
    describe aws_lambda do
      it { should exist}    
      its ('handler') { should eq 'main.on_event'}
      its ('version') { should eq '$LATEST' }
      its ('runtime') { should eq 'python3.7' }
    end
````    

## Parameters

This resource expects the name of the function.


`Propertie`

: All properties as defined by the [Aws::lambda::Types::GetFunctionResponse](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/Lambda/Types/GetFunctionResponse.html)

## Examples


**tests that all lambdas with a particular tag is correctly deployed.**

````

    describe aws_lambda('my_new_lambda') do
        it { should exist}    
        its ('handler') { should eq 'main.on_event'}
        its ('version') { should eq '$LATEST' }
        its ('runtime') { should eq 'python3.7' }
    end
  }

````

## Matchers

This InSpec audit resource uses the standard matchers.  For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).


## AWS Permissions

{{% aws_permissions_principal action="Lambda:Client:GetFunctionResponse" %}}

You can find detailed documentation at [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-api-permissions-ref.html)

