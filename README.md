# Take Home Exercise

-------

# Table of Contents

1. [Compromised AWS Account Credentials](#compromised-aws-account-credentials)
   
   1.1. [Sequence Diagram](#the-following-diagram-provides-a-visual-representation-of-the-steps-described-above)
2. [Technical Writing Guide](#technical-writing-guide)
   
   2.1. [Documentation Deliverables](#documentation-deliverables)
   
   2.2. [Basic Guidelines](#guidelines)
        
       2.1.1. [Keep it Simple](#keep-it-simple)

   2.3. []
3. [API Documentation](#api-documentation-template)

---

## Compromised AWS Account Credentials

Infosec has identified a security incident related to AWS credentials leakage. Execute the procedure below in order to either contain or prevent a possible attack.


1. **Remove all permissions from the affected AWS user without revoking credentials:**

   1.1. Find a user with admin IAM permissions:
```nu sec iam show group infosec-permissions-admin```

   1.2. Request the removal of all the inline policies from the affected IAM user:
```nu iam disallow <user> Source```

   1.3. Request a list of all IAM groups the affected user is included:
   ```nu sec iam show <user>```

   1.4. Request the removal of the affected user from all listed groups:
   ```nu sec iam remove <user> <groups>```


2. **Communicate the incident to the relevant stakeholders.**

3. **Notify the affected user on Slack, as follows:**

*"Your AWS permissions have been temporarily suspended pending an investigation into a possible compromise. If you have any questions, do not hesitate to contact me and, for security reasons, please keep the incident private until further notice from Infosec"*


4. **Send a message through the affected user's Slack to their Manager.**

*"There has been wrongful activity involving this engineer's AWS account. Please inform them that the permissions associated with it have been temporarily blocked and guide them through further understanding of the incident. Also, advise them to keep the incident private until further notice from Infosec"*

5. **Request an admin IAM user (see step 1.1.) to revoke the affected AWS credentials and disable/delete the affected credentials using the AWS console.**

6. **Generate new credentials and a new keypair via AWS console.**

7. **Send the new keypair to the affected user via Slack direct message and instruct them to update all references to their AWS keys, such as the ones in the `.bash_profile`. It is possible to perform this action by using the `nudev ./setupnu.sh`, available at [Setup nudev](https://github.com/nubank/nudev/blob/master/setupnu.sh) or [Nu Setup](https://github.com/nubank/nu-setup).**


#### The following diagram provides a visual representation of the steps described above:

![compromised credentials](https://github.com/tiannamen/ic5-techwriting/blob/main/resources/uml-diagram.jpeg)


Refer to the [AWS Java Developer Guide](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) for information on how to work with AWS credentials and to the [Prescriptive Guide](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-startup-security-baseline/controls-acct.html) for information on how to secure your account.

---

## Technical Writing Guide

Every technical documentation must communicate with the product user in a clear and simplified way, connecting them to the product. 

This guide contains the basics to start writing and delivering technical documentation. The target audience is truly anyone who is interested in bringing additional value to their tech product, by having a documentation. 

For more information regarding the value of documentation, refer to [Google Developers](https://developers.google.com/tech-writing/resources#the_value_of_documentation).

### Documentation Deliverables

The Technical Writing work results in technical documentation, which can be of many types, such as:

- [User manuals](https://redocly.com/docs/developer-portal/guides/)
- [Configuration and installation manuals](https://redocly.com/docs/developer-portal/configuration/)
- [FAQ and troubleshooting guides](https://aws.amazon.com/premiumsupport/knowledge-center/?ref=docs_gateway/index.html)
- [Release notes](https://docs.digibee.com/documentation/release-notes/release-notes-2022/october)
- [API documentation](https://tiannamen.redoc.ly/)
- [Tutorial videos](https://docs.digibee.com/documentation/build/canvas#h_466422e681)

For more information on different types of writing, refer to [UX Design Bootcamp](https://bootcamp.uxdesign.cc/copywriter-content-writer-technical-writer-ux-writer-who-to-hire-2cec63e29488).

### Guidelines

This section provides useful information on some important concepts to have in mind when creating technical content.

#### Keep it Simple

The simpler, the better. Always have in mind that the user does not need some big and complex words to understand the content, actually it is the opposite. Simplify all you can, fitting the complex information into one readable document.

Also, be careful with the paragraphs lenght. Each paragraph should contain only one topic of information, broke into sentences.

#### Target Audience

One of the first definitions for the documentation is the target audience. That is because we must choose the best options to comunicate with our readers. For example, an external documentation should provide information about product usage to the end-user, while internal documentation should provide information about product maintenance. This changes not only the content, but also the tone of voice used in the documentation.

#### Tone of Voice and Style

Companies usually define the tone of voice they want to use to communicate with clients. Here, at Nu, is no different. 

In addition, we also have a style guide, which has the purpose of standardizing our deliveries. Having the same standards, such as colors, fonts, structure etc, brings a feeling of something familiar, which helps Nu bond with its clients.

Make sure your content complies with the [Nu Tone of Voice](), and the [NuDocs Style Guide](), especially in documentations designed to end-users.

#### Table of Contents

This element will help you structure the content and ensure that the reader can easily navigate through the documentation and find the needed information.

#### Know your Grammar

Do not worry: nobody expects you to write like a Technical Writer if you are not. However, you should at least be able to write gramatically correct sentences and paragraphs. In case this is still a challenge to you, check out the [Tech Writing courses from Google Developers](#helpful-links).

### Getting Started

The documentation process usually have 5 stages, as taught by Kieran Morgan in the book *Technical Writing Process*: plan, structure, write, review and publish. Each step covers an indispensable part of the documentation process.

The following image, taken out from the book, exemplifies each step of the process:

![technical writing process](https://github.com/tiannamen/ic5-techwriting/blob/main/resources/technical-writing-process.jpg)

To simplify your journey through this process, we provide a checklist to each step.

#### Plan

1. 



- 
- Table of contents

### Helpful Links

Learn more about Technical Writing and Technical Documentation:

- [Technical Writing - Google Developers](https://developers.google.com/tech-writing)
- [I'd Rather Be Writing Blog](https://idratherbewriting.com/)
- [Write the Docs](https://www.writethedocs.org/)


---

# API Documentation

> For detailed information, refer to the [API Specification on Redoc](https://tiannamen.redoc.ly/).*

*Available until November 22th. After that, it will only be visible with a Redoc user login.

## Nu Accounts

API documentation for the `getAccount` method.

### Retrieve Account

The `getAccount` method retrieves a Nu Account by its identification number. The information retrieved from the account includes:

* Balance
* Document
* Status
* Document Type
* Credit Limit
* Last Update
* Creation Date
* Description
* Available Credit
* Pre-Authorized Credit
* e-mail
* Tolerance
* Available Tolerance

#### Parameters

The Retrieve Account API contains the following parameter:

|PARAMETER|DESCRIPTION|TYPE|REQUIRED|
|---|---|---|---|
|`accountId`|Account identification number.|integer|yes|


#### Request payload

The following snippet is a Java request sample:

**METHOD:** `getAccount`

```
import java.net.*;
import java.net.http.*;
import java.util.*;
import java.nio.charset.StandardCharsets;
import java.util.stream.Collectors;

public class App {
  public static void main(String[] args) throws Exception {
    var httpClient = HttpClient.newBuilder().build();

    HashMap<String, String> params = new HashMap<>();
    params.put("accountId", "0");

    var query = params.keySet().stream()
      .map(key -> key + "=" + URLEncoder.encode(params.get(key), StandardCharsets.UTF_8))
      .collect(Collectors.joining("&"));

    var host = "https://sampleapi.com.br";
    var pathname = "/api/account";
    var request = HttpRequest.newBuilder()
      .GET()
      .uri(URI.create(host + pathname + '?' + query))
      .header("appKey", "YOUR_API_KEY_HERE")
      .build();

    var response = httpClient.send(request, HttpResponse.BodyHandlers.ofString());

    System.out.println(response.body());
  }
}
```

#### Response Payload

* **200 - Successfully returned**

```
{
"id": "string",
"balance": 0,
"document": "string",
"status": "string",
"documentType": "string",
"creditLimit": 0,
"updateAt": "string",
"createdAt": "string",
"description": "string",
"availableCredit": 0,
"preAuthorizedCredit": 0,
"email": "string",
"tolerance": "string",
"availableTolerance": 0
}
```

* **400 - Invalid request**

```
{
"Message": "string"
}
```


