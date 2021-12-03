+++
title = "aws_lambdas Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_lambdas"
identifier = "inspec/resources/aws/aws_lambdas Resource"
parent = "inspec/resources/aws"
+++

<div class="admonition-note">
<p class="admonition-note-title">Audit Section</p>
<div class="admonition-note-text">
<p>Source page: <a href="https://github.com/inspec/inspec-aws/blob/main/docs/resources/aws_lambdas.md">aws_lambdas.md</a></p>
<p>Edited page: <a href="https://github.com/ianmadd/inspec-aws/blob/im/hugo/docs-chef-io/content/inspec/resources/aws_lambdas.md">aws_lambdas.md</a></p>
</div>
</div>



Use the `aws_lambdas` resource to test the collection of lambdas deployed into an account.

## Installation

{{% inspec_aws_install %}}

## Syntax

````
    describe aws_lambdas do
      its('count') { should eq 20 }
    end
````    

## Parameters

This resource does not expect any parameters.


## Properties

`names`
: The names of the lambda deployed.

`tags`
: The tags of the lambda deployed.

## Examples


**tests that all lambdas with a particular tag is correctly deployed.**

````
  lambdas = aws_lambdas() 

  describe lambdas do
    its ('count') { should eq 33}    
  end

  lambdas.tags.each_with_index { | tag, i |    
    if tag!= {} and tag.include? 'Application' and tag['Application']=='test')
      lambda_name = lambdas.names[i]

      describe aws_lambda(lambda_name) do
          it { should exist}    
          its ('handler') { should eq 'main.on_event'}
          its ('version') { should eq '$LATEST' }
          its ('runtime') { should eq 'python3.7' }
      end
    end
  }

````

## Matchers

This InSpec audit resource uses the standard matchers.  For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).


## AWS Permissions

{{% aws_permissions_principal action="Lambda:Client:ListFunctionsResponse" %}}

You can find detailed documentation at [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-api-permissions-ref.html)

