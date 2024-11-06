# API-Note

https://editor.swagger.io/

https://www.openapis.org/

https://github.com/public-apis/public-apis

## Calling API Instructions

Here’s a guide on different ways to call a web API using various tools and libraries in popular programming languages. Each approach includes sample code for `curl`, HTTP client libraries, and REST API calls.

---

## 1. **Using `curl` in the Command Line**

`curl` is a powerful command-line tool for making HTTP requests and interacting with web APIs.

```bash
# Basic GET request
curl -X GET "https://api.example.com/resource"

# POST request with JSON data
curl -X POST "https://api.example.com/resource" -H "Content-Type: application/json" -d '{"key":"value"}'
```

## 2. **Python**

### Using `requests` Library

```python
import requests

# GET request
response = requests.get("https://api.example.com/resource")
print(response.json())

# POST request with JSON data
data = {"key": "value"}
response = requests.post("https://api.example.com/resource", json=data)
print(response.json())
```

### Using `http.client`

```python
import http.client
import json

conn = http.client.HTTPSConnection("api.example.com")
headers = {"Content-Type": "application/json"}
conn.request("POST", "/resource", body=json.dumps({"key": "value"}), headers=headers)

response = conn.getresponse()
print(response.read().decode())
conn.close()
```

## 3. **JavaScript**

### Using `fetch` API (Browser or Node.js)

```javascript
// GET request
fetch("https://api.example.com/resource")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// POST request
fetch("https://api.example.com/resource", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ key: "value" })
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

### Using Axios (Node.js and Browser)

```javascript
const axios = require("axios");

// GET request
axios.get("https://api.example.com/resource")
  .then(response => console.log(response.data))
  .catch(error => console.error(error));

// POST request
axios.post("https://api.example.com/resource", { key: "value" })
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
```

## 4. **Java**

### Using `HttpURLConnection`

```java
import java.io.*;
import java.net.*;
import java.nio.charset.StandardCharsets;

public class ApiRequestExample {
    public static void main(String[] args) throws IOException {
        URL url = new URL("https://api.example.com/resource");
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");

        BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String inputLine;
        StringBuilder content = new StringBuilder();
        while ((inputLine = in.readLine()) != null) {
            content.append(inputLine);
        }
        in.close();
        System.out.println(content.toString());
    }
}
```

### Using `HttpClient` (Java 11+)

```java
import java.net.http.*;
import java.net.URI;
import java.util.Map;
import com.fasterxml.jackson.databind.ObjectMapper;

public class ApiRequestExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
            .uri(new URI("https://api.example.com/resource"))
            .GET()
            .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

## 5. **C#**

### Using `HttpClient`

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

class Program
{
    private static readonly HttpClient client = new HttpClient();

    static async Task Main()
    {
        // GET request
        var response = await client.GetStringAsync("https://api.example.com/resource");
        Console.WriteLine(response);

        // POST request
        var data = new StringContent("{\"key\":\"value\"}", Encoding.UTF8, "application/json");
        var postResponse = await client.PostAsync("https://api.example.com/resource", data);
        Console.WriteLine(await postResponse.Content.ReadAsStringAsync());
    }
}
```

## 6. **Ruby**

### Using `Net::HTTP`

```ruby
require 'net/http'
require 'json'
require 'uri'

# GET request
uri = URI('https://api.example.com/resource')
response = Net::HTTP.get(uri)
puts response

# POST request
uri = URI('https://api.example.com/resource')
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
request = Net::HTTP::Post.new(uri.path, 'Content-Type' => 'application/json')
request.body = { key: 'value' }.to_json
response = http.request(request)
puts response.body
```

## 7. **PHP**

### Using `file_get_contents` (for simple requests)

```php
<?php
$response = file_get_contents("https://api.example.com/resource");
echo $response;
?>
```

### Using `cURL` (PHP)

```php
<?php
$curl = curl_init("https://api.example.com/resource");
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($curl);
curl_close($curl);
echo $response;

// POST request
$curl = curl_init("https://api.example.com/resource");
$data = json_encode(['key' => 'value']);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
curl_setopt($curl, CURLOPT_HTTPHEADER, ['Content-Type:application/json']);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($curl);
curl_close($curl);
echo $response;
?>
```

## 8. **Go**

### Using `net/http` Package

```go
package main

import (
	"bytes"
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	// GET request
	resp, err := http.Get("https://api.example.com/resource")
	if err != nil {
		fmt.Println(err)
		return
	}
	defer resp.Body.Close()
	body, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))

	// POST request
	jsonData := []byte(`{"key": "value"}`)
	resp, err = http.Post("https://api.example.com/resource", "application/json", bytes.NewBuffer(jsonData))
	if err != nil {
		fmt.Println(err)
		return
	}
	defer resp.Body.Close()
	body, _ = ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```

Each code example above demonstrates basic GET and POST requests in various languages, highlighting commonly used methods for interacting with web APIs.

## References

Certainly! Here are some authoritative resources and references for web API usage in different languages, including documentation for the libraries and tools mentioned in the examples.

---

### 1. **curl**

- **curl Documentation**: [https://curl.se/docs/](https://curl.se/docs/)

### 2. **Python**

- **requests Library**: [Python requests Documentation](https://requests.readthedocs.io/en/latest/)
- **http.client Module**: [Python http.client Documentation](https://docs.python.org/3/library/http.client.html)

### 3. **JavaScript**

- **fetch API**: [MDN Web Docs on Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- **Axios**: [Axios GitHub Repository](https://github.com/axios/axios) and [Axios Documentation](https://axios-http.com/)

### 4. **Java**

- **HttpURLConnection**: [Oracle Java HttpURLConnection Documentation](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)
- **HttpClient (Java 11+)**: [Java HttpClient Documentation (Java SE 11)](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html)

### 5. **C#**

- **HttpClient Class**: [Microsoft .NET HttpClient Documentation](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httpclient?view=net-7.0)

### 6. **Ruby**

- **Net::HTTP Library**: [Ruby Net::HTTP Documentation](https://docs.ruby-lang.org/en/3.0.0/Net/HTTP.html)

### 7. **PHP**

- **file_get_contents Function**: [PHP file_get_contents Documentation](https://www.php.net/manual/en/function.file-get-contents.php)
- **cURL in PHP**: [PHP cURL Documentation](https://www.php.net/manual/en/book.curl.php)

### 8. **Go**

- **net/http Package**: [Go net/http Documentation](https://pkg.go.dev/net/http)

---

## Addtional Ways to invoke Web API call

Here are the references and documentation for each of the methods mentioned above, which will help you dive deeper into using these tools and techniques for making REST API calls.

---

Certainly! Here’s how to invoke REST APIs using PowerShell, Postman, and some other less common ways, such as using desktop automation tools or embedded scripts in applications.

---

## 1. **PowerShell**

PowerShell is a powerful scripting language and shell that allows direct HTTP requests to REST APIs.

### Using `Invoke-RestMethod` (PowerShell 3.0+)

```powershell
# GET request
Invoke-RestMethod -Uri "https://api.example.com/resource" -Method Get

# POST request with JSON data
$headers = @{ "Content-Type" = "application/json" }
$body = @{ "key" = "value" } | ConvertTo-Json
Invoke-RestMethod -Uri "https://api.example.com/resource" -Method Post -Headers $headers -Body $body
```

### Using `Invoke-WebRequest` (alternative option)

```powershell
# GET request
Invoke-WebRequest -Uri "https://api.example.com/resource" -Method Get

# POST request with JSON data
$headers = @{ "Content-Type" = "application/json" }
$body = @{ "key" = "value" } | ConvertTo-Json
Invoke-WebRequest -Uri "https://api.example.com/resource" -Method Post -Headers $headers -Body $body
```

---

## 2. **Postman**

Postman is a popular GUI tool for testing and interacting with REST APIs. Here’s how to use it:

1. **Open Postman**: Create a new request.
2. **Set the Request Type**:
   - Select GET, POST, PUT, DELETE, etc., from the dropdown next to the URL field.
3. **Enter the API URL**: Type the URL for the API endpoint (e.g., `https://api.example.com/resource`).
4. **Add Headers**:
   - In the "Headers" tab, set headers such as `Content-Type: application/json`.
5. **Add Request Body (for POST requests)**:
   - In the "Body" tab, select "raw" and choose "JSON" from the dropdown. Enter the JSON payload, like `{"key": "value"}`.
6. **Send the Request**:
   - Click "Send" to execute the request. The response will appear below.

### Postman CLI (Newman)

Postman also has a CLI, `newman`, that allows you to run Postman collections directly from the command line, useful for testing automation.

```bash
# Run a Postman collection
newman run path/to/collection.json
```

---

## 3. **cURL in Scripts and Other Applications**

`curl` is often embedded in shell scripts and other applications for API automation. Here’s how you can call REST APIs with `curl` in a script.

### Bash Script with cURL (Linux/macOS)

```bash
#!/bin/bash

# Define variables
url="https://api.example.com/resource"
json_data='{"key": "value"}'

# GET request
curl -X GET "$url"

# POST request
curl -X POST "$url" -H "Content-Type: application/json" -d "$json_data"
```

### Embedding cURL in Desktop Applications (e.g., Automator on macOS)

1. Open **Automator** and create a new workflow.
2. Add a **"Run Shell Script"** action.
3. Use the `curl` command within this action.
4. Run the workflow to execute the HTTP request.

---

## 4. **Using Node-RED**

Node-RED is an open-source flow-based development tool for visual programming. You can create workflows to automate HTTP requests.

1. **Install Node-RED** and start the interface.
2. **Add HTTP Request Node**: Drag an HTTP request node into the workspace.
3. **Configure the HTTP Node**:
   - Set the method to GET, POST, etc.
   - Enter the API endpoint URL and any required headers or body data.
4. **Deploy and Run**: Connect the HTTP node to an output node (e.g., debug node) and deploy the flow.

---

## 5. **Zapier or Integromat (now Make)**

Zapier and Integromat (Make) are automation platforms that can connect to APIs without code.

1. **Create a Zap or Scenario**:
   - Set up a new workflow to trigger on schedule or based on another app.
2. **Add a Webhooks/HTTP Request Action**:
   - Choose Webhooks by Zapier or HTTP request in Make.
3. **Configure the Request**:
   - Enter the endpoint URL and configure the request type (GET, POST, etc.).
   - Add any headers or JSON body as needed.

---

## 6. **Using SQL Server (T-SQL with `sp_invoke_external_rest_endpoint`)**

Some modern databases support direct HTTP calls. Here’s how to use a REST API within SQL Server using the new `sp_invoke_external_rest_endpoint`.

```sql
DECLARE @Response NVARCHAR(MAX);
EXEC sp_invoke_external_rest_endpoint
    @method = 'GET',
    @url = 'https://api.example.com/resource',
    @response = @Response OUTPUT;

SELECT @Response;
```

> **Note**: `sp_invoke_external_rest_endpoint` is a recent addition in SQL Server and requires specific configurations for permissions and network access.

---

## 7. **Power Automate (Microsoft Power Platform)**

Power Automate allows HTTP requests and workflows without coding, especially within the Microsoft ecosystem.

1. **Create a New Flow**: Start a new flow in Power Automate.
2. **Add HTTP Action**:
   - Search for the HTTP action and add it to the flow.
3. **Configure the Request**:
   - Enter the URL, request type (GET, POST, etc.), and any headers or JSON body.
4. **Run the Flow**: Execute the flow or schedule it as needed.

---

## 8. **RPA Tools (e.g., UiPath, Automation Anywhere)**

Robotic Process Automation (RPA) tools can interact with APIs for backend automation.

### UiPath Example

1. **Drag an HTTP Request Activity** into your UiPath workflow.
2. **Configure the Activity**:
   - Set the endpoint URL, HTTP method, and any headers or body data.
3. **Execute the Workflow**: Run the UiPath workflow to make the API request and process the response.

---

## 9. **Java Spring Boot RestTemplate (Java Framework)**

In a Java Spring Boot application, you can use `RestTemplate` to call REST APIs.

```java
import org.springframework.web.client.RestTemplate;

public class ApiService {
    private RestTemplate restTemplate = new RestTemplate();

    public String callApi() {
        String url = "https://api.example.com/resource";
        return restTemplate.getForObject(url, String.class);
    }
}
```

This is typically used within backend applications built with Java and Spring Boot.

---

Each of these methods provides unique ways to interact with REST APIs, enabling integration across a wide variety of platforms and environments.

## References

### 1. **PowerShell**

- **Invoke-RestMethod Documentation**: [Microsoft PowerShell Docs - Invoke-RestMethod](https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/rest-api?view=powershell-7.1#invoke-restmethod)
- **Invoke-WebRequest Documentation**: [Microsoft PowerShell Docs - Invoke-WebRequest](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.1)

### 2. **Postman**

- **Postman Documentation**: [Postman Learning Center](https://learning.postman.com/docs/getting-started/introduction/)
- **Newman CLI for Postman**: [Newman Documentation](https://learning.postman.com/docs/continuous-integration/using-newman-cli/)

### 3. **cURL in Scripts**

- **curl Documentation**: [curl Documentation](https://curl.se/docs/)
- **Shell Scripting Basics (Bash)**: [GNU Bash Documentation](https://www.gnu.org/software/bash/manual/bash.html)

### 4. **Node-RED**

- **Node-RED Documentation**: [Node-RED User Guide](https://nodered.org/docs/user-guide/)
- **Node-RED HTTP Request Node Documentation**: [HTTP Request Node](https://nodered.org/docs/user-guide/nodes#http-request)

### 5. **Zapier and Integromat (Make)**

- **Zapier Webhooks Documentation**: [Zapier Webhooks](https://zapier.com/page/webhooks/)
- **Make (Integromat) HTTP Request Module**: [Make Documentation - HTTP Request](https://www.make.com/en/help/app/http)

### 6. **SQL Server (T-SQL with `sp_invoke_external_rest_endpoint`)**

- **sp_invoke_external_rest_endpoint Documentation**: [Microsoft Documentation for SQL Server REST](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-invoke-external-rest-endpoint-transact-sql)
- **Using HTTP with SQL Server**: [Microsoft Documentation - External REST Endpoints](https://learn.microsoft.com/en-us/sql/connect/sql-db-query?view=sql-server-ver15)

### 7. **Power Automate (Microsoft Power Platform)**

- **Power Automate Documentation**: [Microsoft Power Automate Documentation](https://learn.microsoft.com/en-us/power-automate/overview)
- **HTTP Connector in Power Automate**: [HTTP with Azure Power Automate](https://learn.microsoft.com/en-us/power-automate/custom-connectors/define-blank)

### 8. **RPA Tools (UiPath)**

- **UiPath HTTP Request Activity Documentation**: [UiPath Documentation - HTTP Request](https://docs.uipath.com/activities/docs/http-request)
- **Automation Anywhere REST Web Services**: [Automation Anywhere Documentation](https://docs.automationanywhere.com/)

### 9. **Java Spring Boot RestTemplate**

- **RestTemplate in Spring Framework**: [Spring Docs - RestTemplate](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/RestTemplate.html)
- **Spring Boot Guide**: [Spring Boot Guide - Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)

---

These references provide detailed information, examples, and best practices for using each tool and method to make REST API calls effectively.

These resources will give you comprehensive information about each language's HTTP handling capabilities and provide further examples and advanced features.
