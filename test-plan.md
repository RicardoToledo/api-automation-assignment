# Test plan

- [Test scope](#test-scope)
  * [Objective](#objective)
  * [Approach and selection](#approach-and-selection)
  * [Determining priority level](#determining-priority-level)
- [Test Suite](#test-suite)
- [Test deliverables](#test-deliverables)
  * [Found bugs](#found-bugs)
- [Improvements / Next steps](#improvements--next-steps)
  
## Test scope

### Objective

To test that all Petstore API's endpoints respond with successful status code as expected using test positive scenarios.

### Approach and selection

> What you used to select the scenarios, what was your approach?

I focused on:
- At least test the positive test case of each endpoint in the API.
- Guarantee that all the CRUD operations were covered.
- Covering a full happy path flow or E2E for the API.

### Determining priority level

> - You have listed the most important scenarios to automate (minimal 3 API and 3 Web)
> - Why are they the most important?

| Description | Priority |
|:--|--|
| Endpoints performing critical CRUD operations which can't be replaced by another endpoint or workaround | High |
| Endpoints performing non-critical CRUD operations which can be replaced using another endpoint that in some way can obtain the same result | Medium |
| Endpoints performing least critical CRUD operations which will not affect the functionality flow | Low |

**Answer:** The most important scenario is the minimum happy path which is composed of 15 test cases of high priority. 

## Test Suite

This suite is composed of all endpoints and can be considered as a full happy path or E2E.

| Group | ID     | Method | Request                                      | Expected response code | Status   | Priority |
| ----- | ------ | ------ | -------------------------------------------- | ---------------------- | -------- | -------- |
| Pet   | API.01 | POST   | Add a new pet to the store                   | 200                    | Passed   | High     |
|       | API.02 | PUT    | Update an existing pet                       | 200                    | Passed   | High     |
|       | API.03 | GET    | Finds Pets by status available               | 200                    | Passed   | Medium   |
|       | API.04 | GET    | Finds Pets by status pending                 | 200                    | Passed   | Medium   |
|       | API.05 | GET    | Finds Pets by status sold                    | 200                    | Passed   | Medium   |
|       | API.06 | GET    | Finds Pets by unregistered status            | 200                    | Passed   | Medium   |
|       | API.07 | GET    | Find pet by ID                               | 200                    | Unstable | High     |
|       | API.08 | POST   | Updates a pet in the store with form data    | 200                    | Passed   | Medium   |
|       | API.09 | POST   | Upload pet's image                           | 200                    | Unstable | Low      |
|       | API.10 | DELETE | Deletes a pet                                | 200                    | Passed   | High     |
| Store | API.11 | POST   | Add a new pet to the store                   | 200                    | Passed   | High     |
|       | API.12 | POST   | Place an order for a pet                     | 200                    | Passed   | High     |
|       | API.13 | GET    | Find purchase order by ID                    | 200                    | Unstable | High     |
|       | API.14 | DELETE | Delete purchase order by ID                  | 200                    | Unstable | High     |
|       | API.15 | GET    | Returns pet inventories by status            | 200                    | Passed   | High     |
| User  | API.16 | POST   | Create user                                  | 200                    | Passed   | High     |
|       | API.17 | POST   | Creates list of users with given input array | 200                    | Passed   | Medium   |
|       | API.18 | POST   | Creates list of users with given input array | 200                    | Passed   | Medium   |
|       | API.19 | PUT    | Updated user                                 | 200                    | Passed   | High     |
|       | API.20 | GET    | Logs user into the system                    | 200                    | Passed   | High     |
|       | API.21 | GET    | Find logged in user by username              | 200                    | Passed   | High     |
|       | API.22 | GET    | Logs out current logged in user session      | 200                    | Passed   | Medium   |
|       | API.23 | DELETE | Delete user                                  | 200                    | Unstable | High     |

## Test deliverables

| Title | Description |
| ------ | ------- |
| Test repository | A repository containing the code, scripts, and documentation necessary to run the tests |
| Test plan | Document containing test scope, approach, and test suite |

### Found bugs

On API:
- High severity: Inconsistent response on all endpoints using an object with ID as a parameter.
- A pet can be created with an empty object
- Updating a pet with invalid ID or obdy will generate same pet updated
- New Pet status can be added with all POST and PUT requests

On Calliope.Pro: 
- Possible bug: issue on JSON parser/parsing process, after JSON report in .zip is imported using a POST request on its API the report shows every result duplicated. Observed during CI/CD workflow with the expected number of requests and execution output.

## Improvements / Next steps

> What could be the next steps to your project

- Definitely increase coverage:
	- Explore this very interesting approach that I was unable to do due to lack of time.
		- https://www.tjmaher.com/2019/06/notes-amber-race-exploring-service-apis.html
		- https://testautomationu.applitools.com/exploring-service-apis-through-test-automation/chapter3.0.html
	- Add negative and edge test cases: I left a couple of examples on some requests on what other possible response scenarios we should test in the future or as TODO
	- Validate schema and response's body elements
- Explore performance testing and concurrency capabilities
- Filtering my tests
- Ongoing code maintenance to keep it clean and scalable.
