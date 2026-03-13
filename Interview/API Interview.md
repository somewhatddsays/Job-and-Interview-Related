# API Interview
## Questions with In-Depth Practical Answers (For QA)
###  **Ul works fine but API response data is incorrect. How will you investigate?** <br>
First, I will capture the exact API request from browser DevTools or network logs to validate the request payload, headers, and query parameters.
Then, I will execute the same API in Postman to confirm whether the issue exists independently of UI.
Next, I will compare the API response with the Swagger/OpenAPI contract to ensure fields, data types, and structure are correct.
If mismatch persists, I will validate database records using SQL queries to confirm whether incorrect data is stored or transformation logic is failing.
Finally, I will check backend logs to identify mapping issues, caching problems, or business rule failures before reporting with proper evidence.

---

###  **API is returning 500 error intermittently. What steps will you take?** <br>
Intermittent 500 errors usually indicate backend instability or dependency failures.
First, I will try reproducing the issue with the same payload multiple times.
Then I will check server logs and stack traces to identify null pointer exceptions, timeout errors, or database failures.
I will validate whether dependent services (third-party APIs, microservices) are responding properly.
Next, I will analyze system load, memory spikes, and thread pool exhaustion.
Finally, I will document frequency, payload samples, and logs to help developers identify root cause quickly.

---

###  **How will you test APIs when frontend is not yet developed?** <br>
APIs can be tested independently using Postman, RestAssured, or similar tools.
I will validate request methods (GET, POST, PUT, DELETE), status codes, and response structure.
Schema validation will ensure response matches contract.
I will design boundary value tests, negative tests (invalid payload, missing headers), and security tests (unauthorized access).
If dependent APIs are unavailable, I will use mocks or stubs to simulate responses.

---

###  **Response time suddenly increased in production. How will you validate and report it?** <br>
First, I will compare current response time with historical metrics using monitoring tools.
Then I will replicate issue in staging using performance tools like JMeter.
I will analyze slow database queries, missing indexes, or inefficient joins.
I will verify caching layers and external service delays.
Finally, I will create a detailed report including average response time, peak latency, logs, and possible impact.

---

###  **Developer says 'API works on my machine.' What will you check?** <br>
I will compare environment configurations such as base URL, DB version, API version, and feature flags. Then I will verify request headers, authentication tokens, and payload format.
I will check whether local environment has mock services enabled.
Next, I will reproduce issue in shared environment and provide exact request/response logs.
Clear evidence helps move discussion from opinion to facts.

---

###  **How will you validate that API data is correctly stored in database?** <br>
After API execution, I will capture response ID or reference number.
Using SQL queries, I will validate that records exist in correct tables. I will verify column mapping, relationships, timestamps, and status flags. For update/delete operations, I will confirm correct state change.
If available, I will validate audit logs and history tables.

---

###  **How do you handle dynamic authentication tokens in automation?** <br>
In automation framework, I will create a login API method that captures access token from response.
The token will be stored in a global variable or session object.
All subsequent API requests will dynamically use this token in Authorization header.
If token expires, refresh token API will be triggered automatically.
This ensures tests remain independent and environment-ready.

---

###  **You need to test multiple dependent APIs (chained flow). How will you design automation?** <br>
I will design modular API methods for each endpoint.
Response data from API1 (e.g., userld) will be extracted and passed dynamically to AP12.
Assertions will validate each step before proceeding.
Test data cleanup will be handled at end to maintain environment stability.
Proper logging ensures easy debugging in case of failure.

---

###  **How will you test API rate limiting and throttling?** <br>
I will send high volume of requests within short duration using scripts or performance tools.
Then I will validate 429 status code and retry-after headers.
I will verify that system blocks excess requests while still allowing valid traffic.
I will also check whether rate limit resets after defined time window.

---

###  **How will you ensure API automation runs reliably in CI/CD pipeline?** <br>
Tests should be environment-independent and avoid hardcoded values.
I will implement configuration management for different environments.
Retry logic will handle transient failures but not hide real defects.
Reports and logs must be detailed for debugging.
Smoke suite should run on every build, regression on scheduled basis.



**Original Poster**: [thetestingacademy](https://www.instagram.com/thetestingacademy/)