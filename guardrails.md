
# Creating guardrails in the AWS Console

If running from your own account, please complete the Prerequisites section before starting this lab.

[Prerequisites](/building-with-amazon-bedrock/en-US/prerequisites/)

Final product:



![Screenshot of guardrails being tested in AWS Console](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-test-trace.png)

 

[Lab introduction](#lab-introduction)

# Lab introduction

---

In this lab, we will walk through the manual creation and testing of a guardrail using the AWS Console.

In addition to manual creation, there are multiple ways to automate the creation of guardrails, including SDKs, infrastructure-as-code, and CLI commands.

- AWS API documentation: https://docs.aws.amazon.com/bedrock/latest/APIReference/API_CreateGuardrail.html 

- AWS CLI documentation: https://docs.aws.amazon.com/cli/latest/reference/bedrock/create-guardrail.html 

- AWS CloudFormation documentation: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-bedrock-guardrail.html 

- Terraform documentation (awscc): https://registry.terraform.io/providers/hashicorp/awscc/latest/docs/resources/bedrock_guardrail 

[https://docs.aws.amazon.com/bedrock/latest/APIReference/API_CreateGuardrail.html ](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_CreateGuardrail.html)

[https://docs.aws.amazon.com/cli/latest/reference/bedrock/create-guardrail.html ](https://docs.aws.amazon.com/cli/latest/reference/bedrock/create-guardrail.html)

[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-bedrock-guardrail.html ](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-bedrock-guardrail.html)

[https://registry.terraform.io/providers/hashicorp/awscc/latest/docs/resources/bedrock_guardrail ](https://registry.terraform.io/providers/hashicorp/awscc/latest/docs/resources/bedrock_guardrail)

In the following lab, we will learn how to create guardrails programmatically using the Python Boto3 API 

[Python Boto3 API ](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/bedrock/client/create_guardrail.html)

 

[Guardrail creation walkthrough](#guardrail-creation-walkthrough)

## Guardrail creation walkthrough

We'll start by creating a guardrail with sample configurations for each major component of a guardrail. You will want to design your guardrails based on your specific application's requirements.

1. From the Amazon Bedrock navigation menu, under Safeguards, select Guardrails



![Screenshot of Amazon Bedrock navigation menu](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/menu-guardrails.png)

 

From the Guardrails section, you can review any existing guardrails, edit or delete guardrails, or create new guardrails.

1. Select the Create guardrail button



![Screenshot of Guardrails page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/list-create-guardrail.png)

 

[Provide guardrail details](#provide-guardrail-details)

### Provide guardrail details

The AWS Console guides you through a multi-step guardrail creation process. The first step allows you to provide general details about the guardrail, such as name, a meaningful description, a Customer Managed KMS key, and tags.

1. Set the guardrail details\
\
Set Name to Guardrail-from-Console\
Select the Next button\
\


2. Set Name to Guardrail-from-Console

3. Select the Next button

- Set Name to Guardrail-from-Console

- Select the Next button



![Screenshot of Guardrail details entry page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-details.png)

 

[Configure content filters](#configure-content-filters)

### Configure content filters

The second step allows you to enable and set strength levels for content filters. Content filtering depends on the classification of the user input or model response across the listed categories (Hate, Insults, Sexual, Violence, Misconduct, and Prompt Attack) and the confidence levels (None, Low, Medium, High).  For example, if a user were to ask for instructions on how to hotwire a car, that would likely be classified as Misconduct with a confidence of High.

1. Under Filter strengths for prompts, turn on the Enable filters for prompts toggle\
\
Set the Prompt Attack slider to High\
\


2. Set the Prompt Attack slider to High

- Set the Prompt Attack slider to High



![Screenshot of Guardrail details prompt filters](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-prompt.png)

 

1. Under Filter strengths for responses, turn on the Enable filters for responses toggle



![Screenshot of Guardrails response filters](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-response.png)

 

1. Select the Next button.

 

[Add denied topics](#add-denied-topics)

### Add denied topics

The next step sets any denied topics that should be blocked. In our example, we specify a topic to be detected in user inputs and model responses. You can add up to 30 denied topics. If a user\'92s input or the model response matches the denied topic, a rejection message will be returned to the user.  Optionally, you can also add sample phrases to help the guardrail understand what to look for.

1. Select Add denied topic.\
\
Set Name to Bitcoin\
Set Definition for topic to Providing advice, direction, or examples of how to mine, use, or interact with Bitcoin, including Cryptocurrency-related third-party services.\
\


2. Set Name to Bitcoin

3. Set Definition for topic to Providing advice, direction, or examples of how to mine, use, or interact with Bitcoin, including Cryptocurrency-related third-party services.

- Set Name to Bitcoin

- Set Definition for topic to Providing advice, direction, or examples of how to mine, use, or interact with Bitcoin, including Cryptocurrency-related third-party services.

 

1. Expand the Add sample phrases section. Add the following sample phrases:\
\
How do I mine Bitcoin?\
What is the current value of BTC?\
Which instance is the best for crypto mining?\
Is mining cryptocurrency against the terms?\
How do I maximize my Bitcoin profits?\
Select the Confirm button.\
\


2. How do I mine Bitcoin?

3. What is the current value of BTC?

4. Which instance is the best for crypto mining?

5. Is mining cryptocurrency against the terms?

6. How do I maximize my Bitcoin profits?

7. Select the Confirm button.

- How do I mine Bitcoin?

- What is the current value of BTC?

- Which instance is the best for crypto mining?

- Is mining cryptocurrency against the terms?

- How do I maximize my Bitcoin profits?

- Select the Confirm button.



![Screenshot of Denied topic configuration](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guadrail-denied-topic-modal.png)

 

1. On the Add denied topics page, select the Next button.



![Screenshot of Denied topics list](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-denied-topics.png)

 

[Add word filters](#add-word-filters)

### Add word filters

In this step, we add specific word filters that will be blocked in both user inputs and model responses. Amazon Bedrock Guardrails also offers a pre-defined profanity list that can be enabled. We will enable a globally-defined profanity filter, and add a word filter for our fictional competitor "AnyCompany".

1. \
Configure word filters.\
\
Select the Filter profanity checkbox\
Under View and edit words and phrases, add AnyCompany\
Select the Next button.\
\


2. Select the Filter profanity checkbox

3. Under View and edit words and phrases, add AnyCompany

4. Select the Next button.

Configure word filters.

- Select the Filter profanity checkbox

- Under View and edit words and phrases, add AnyCompany

- Select the Next button.



![Screenshot of the Add word filters page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-add-word-filters.png)

 

[Add sensitive information filters](#add-sensitive-information-filters)

### Add sensitive information filters

Guardrails also allows the capability to redact or mask sensitive information such as Personally Identifiable Information. You can also use Regular Expressions (RegEx) to pattern match on types on information, such as account numbers.

1. Under PII types, select Add new PII.

- \
Add a row for PII Type = Name, with Guardrail Behavior = Mask\


- \
Add a row for PII Type = Email, with Guardrail Behavior = Mask\


- \
Select the Next button\


Add a row for PII Type = Name, with Guardrail Behavior = Mask

Add a row for PII Type = Email, with Guardrail Behavior = Mask

Select the Next button



![Screenshot of Sensitive information page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-pii.png)

 

[Define blocked messaging](#define-blocked-messaging)

### Define blocked messaging

Finally, specific individual messages for blocked user inputs and model responses are added.

1. \
Set the messaging for blocked prompts and responses.\
\
\
Set Messaging for blocked prompts to Apologies, this model cannot be used to discuss inappropriate or off-topic content.\
\
\
Set Messaging for blocked responses to Apologies, the model's response to your request was blocked.\
\
\
Select the Next button\
\
\


2. \
Set Messaging for blocked prompts to Apologies, this model cannot be used to discuss inappropriate or off-topic content.\


3. \
Set Messaging for blocked responses to Apologies, the model's response to your request was blocked.\


4. \
Select the Next button\


Set the messaging for blocked prompts and responses.

- \
Set Messaging for blocked prompts to Apologies, this model cannot be used to discuss inappropriate or off-topic content.\


- \
Set Messaging for blocked responses to Apologies, the model's response to your request was blocked.\


- \
Select the Next button\


Set Messaging for blocked prompts to Apologies, this model cannot be used to discuss inappropriate or off-topic content.

Set Messaging for blocked responses to Apologies, the model's response to your request was blocked.

Select the Next button



![Screenshot of Guardrail messaging page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-messaging.png)

 

[Review and create guardrail](#review-and-create-guardrail)

### Review and create guardrail

In the final step of the creation process, you can review the guardrail details prior to creating it.

1. Review the guardrail and create it.

- Scroll to the bottom of the page, and select Create guardrail



![Screenshot of guardrail review and create page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/review-and-create.png)

 

[Test the draft guardrail](#test-the-draft-guardrail)

## Test the draft guardrail

Once your guardrail has been defined, you can test the guardrail with an Amazon Bedrock model. The AWS Console includes a testing feature where you can enter test prompts and evaluate guardrail actions.

1. From the Guardrails list page, select Guardrail-from-Console



![Screenshot of guardrail list page with new guardrail visible](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/list-with-guardrail.png)

 

1. In the Test panel on the right, select the Select model button.



![Screenshot of Guardrail view page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-view.png)

 

1. Use the Select model dialog to select a model.

- Select Anthropic, then Claude 3 Sonnet

- Select the Apply button



![Screenshot of Guardrail model selection dialog](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-select-model.png)

 

1. Test the guardrail by pasting the following examples into the Prompt box.

Prompt results can be random and change over time. The following prompts worked at the time of writing, but you may need to modify them to see the desired behavior.

A simple, safe prompt should work:

 

This prompt should be blocked at input time:

 

This prompt will likely get the model to talk about Bitcoin in its response, which should get blocked:

 



![Screenshot of Guardrail test response - showing that the model started talking about Bitcoin, and the guardrail blocked the response](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-test-response.png)

 

This is an example of our scenario where we want to prevent our users from asking advice related to Crypto or Bitcoin.  When there is a blocked model response, you can see the model's unfiltered response in the Model response field, and the actual redacted/blocked response in the Final response field.

 

[View the guardrail trace](#view-the-guardrail-trace)

### View the guardrail trace

For each interaction, you can see which of your entered categories that the prompt triggered and what the results of the test were.

1. \
In the Test panel, select the View trace button.\
\
\
Test the guardrail by pasting the following examples into the Prompt box.\
\
\
Depending on the situation, you might see actions captured on either the Prompt or Model response tabs.\
\
\
Use the Prompt tab to see any actions taken based on the user input. Use the Model response tab to see any actions applied to the model\'92s response.\
\
\


2. \
Test the guardrail by pasting the following examples into the Prompt box.\


3. \
Depending on the situation, you might see actions captured on either the Prompt or Model response tabs.\


4. \
Use the Prompt tab to see any actions taken based on the user input. Use the Model response tab to see any actions applied to the model\'92s response.\


In the Test panel, select the View trace button.

- \
Test the guardrail by pasting the following examples into the Prompt box.\


- \
Depending on the situation, you might see actions captured on either the Prompt or Model response tabs.\


- \
Use the Prompt tab to see any actions taken based on the user input. Use the Model response tab to see any actions applied to the model\'92s response.\


Test the guardrail by pasting the following examples into the Prompt box.

Depending on the situation, you might see actions captured on either the Prompt or Model response tabs.

Use the Prompt tab to see any actions taken based on the user input. Use the Model response tab to see any actions applied to the model\'92s response.

The fictional competitor \'93AnyCompany\'94 is a filtered word, so this prompt should be blocked:

 

Hotwiring a car is usually done for criminal purposes, so the Misconduct filter should be triggered:

 

While this statement could be seen as indicative of poor taste, it probably won\'92t trigger the Hate filter:

 

However, the following statement will likely trigger the Hate filter, since we are indicating the hatred of people:

 

Test sensitive information masking:

 

Test a prompt injection attack:

 

Test a jailbreak attack:

 



![Screenshot of Guardrail trace, showing the block due to the mention of Bitcoin in the response](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-test-trace.png)

 

[Create the guardrail version](#create-the-guardrail-version)

## Create the guardrail version

Finally, once your guardrail is aligned with your desired use case, you can create a specific version of the guardrail. When invoking the guardrail, you specify the guardrail ID and the guardrail version you wish to use. This allows you to iterate on additional functionality without impacting any applications currently in use.

1. Under Versions, select the Create version button.



![Screenshot of Guardrail view page](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-view-after-test.png)

 

1. In the Create new version dialog, select the Create version button.



![Screenshot of create new guardrail version dialog](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-create-version.png)

The version will now be listed under the Versions panel.



![Screenshot of guardrail versions panel](https://static.us-east-1.prod.workshops.aws/public/5dd5dc48-363d-4c69-9007-9e5528c5c31f/static/labs/guardrails-create-console/guardrail-version-list.png)

 