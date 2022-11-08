# Take home exercise

-------

# Exercise 1

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

7. **Send the new keypair to the affected user via Slack direct message and instruct them to update all references to their AWS keys, such as the ones in the `.bash_profile`. It is possible to perform this action by using the `nudev ./setupnu.sh`, available at [Nubank Setup - nudev/setupnu](https://github.com/nubank/nudev/blob/master/setupnu.sh) or [Nu Setup](https://github.com/nubank/nu-setup).**

Refer to the [AWS Java Developer Guide](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) for information on how to work with AWS credentials and to the [Prescriptive Guide](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-startup-security-baseline/controls-acct.html) for information on how to secure your account.

### UML Diagram

![compromised credentials](https://github.com/tiannamen/ic5-techwriting/blob/main/resources/uml-diagram.jpeg)

---

# Exercise 2

## Technical Writing Guide



---

# Exercise 3

> For detailed information, refer to the [API Specification on Redoc](https://tiannamen.redoc.ly/).*

*Available until November 22th. After that, it will only be visible with a Redoc user login.

## API Documentation Template

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

```import java.net.*;
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

```{
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

```{
"Message": "string"
}
```


