# API-Note

https://editor.swagger.io/

https://www.openapis.org/

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

These resources will give you comprehensive information about each language's HTTP handling capabilities and provide further examples and advanced features.
