# Software Testing Interview Question and Answer
#### What is Software Testing?
Software testing is the process of validating and verifying a software application to ensure it meet the specified requirements and work as expected by identifying the defects.

#### Why Software Testing is important?
* To find **defects** early
* To ensure **quality** and **reliability**
* Reduce cost of fixing defects
* To improve customer satisfaction

#### Difference between Verification vs Validation
| Verification      | Validation          |
|:------------------|:--------------------|
| Static Testing    | Dynamic Testing     |
| No code execution | Code execution      |
| Done on documents | Done on application |
| Prevents defects  | Finds defects       |

#### Difference between SDLC vs. STLC
| SDLC                              | STLC                           |
|:----------------------------------|:-------------------------------|
| Covers entire project lifecycle   | Covers only testing activities |
| Includes testing as one phase     | Entirely dedicated to testing  |
| Used by dev, test, business teams | Mainly used by test team       |

#### What is SDLC?
SDLC is the software Development Life Cycle that defines phases like:

| Phase                 | Description                                                                                                                 |
|:----------------------|:----------------------------------------------------------------------------------------------------------------------------|
| Requirements analysis | This phase is about **understanding what the customer needs**. Collect requirements like features, rules, and expectations. |
| Design                | This phase is about **how the system will be built**. Create system design, database design, and UI layout.                 |
| Development           | In this phase, developers **write the actual code** based on the design. Front end and Back end happens                     |
| Testing               | This phase checks whether the application **works correctly and is bug-free**.                                              |
| Deployment            | This phase is about **releasing the application to users**.                                                                 |
| Maintenance           | This phase involves **supporting the application after release**. Bug fixes, updates, and enhancements are done here.       |

#### What is STLC?

STLC is the Software Testing Life Cycle that includes

| Phase | Description |
|---|---|
| Requirements analysis | This phase is about **understanding what the customer needs**. Collect requirements like features, rules, and expectations. |
| Test Case Planning | This phase is about **planning how testing will be done**. Test strategy, tools, timeline, resources, and risks. |
| Test Case Design | In this phase, testers **write detailed test cases** based on requirements. |
| Test Environment Setup | This phase is about **preparing the testing environment**. Testers set up hardware, software, browsers, test data, and tools. |
| Test Execution | In this phase, testers **execute the test cases**. They mark test cases as pass or fail and log defects for failures. |
| Test Closure | Testers prepare test summary reports and analyze test results. |

#### Levels of Testing

* **Unit Testing**
  * Testing **individual functions or components**. 
  * Ensuring correct behavior at the smallest level. 
  * Catching errors early. 
  * Performed by **Developers**.

* **Integration Testing**
  * Testing the **interaction between integrated modules**. 
  * Performed by **Developers or Testers**. 
  * To find issues in data flow or communication between modules. 
  * Testing login module integrated with database.

* **System Testing**
  * Full end-to-end testing of the software. 
  * Verifying both functional and non-functional requirements. 
  * Testing the software's behavior. 
  * Performed by **Testers**

* **Acceptance Testing (UAT)**
  * Validating the software against business requirements. 
  * Ensuring the software meets customer expectations. 
  * Getting final approval from the customer. 
  * Performed by **Client / End users / Business team**.


#### What is Smoke Testing?

Smoke testing verifies critical functionalities of the application to ensure the build is stable enough for further testing.\
**Example**: App launch, Login functionality, Home Page

#### What is Sanity Testing?
Sanity testing is performed after minor changes or bug fixes to verify specific functionality works as expected.\
**Example**: Check login functionality works after bug fixes.

####  What is Regression Testing?
Regression testing ensures that new changes or fixes have not broken existing functionality.\
**Example**: Test all login functionality

#### Types of software testing
```
- Types of Software Testing
  - Manual Testing
    - White Box
    - Black Box
      - Functional Testing
        - Unit Testing
        - Integration Testing
        - System Testing
          - Incremental Testing
            - Top-down
            - Bottom-up
          - Non-Incremental Testing
      - Non-Functional Testing
        - Performance Testing
          - Load Testing
          - Stress Testing
          - Scalability Testing
          - Stability Testing
        - Usability Testing
        - Compatibility Testing
    - Grey Box
  - Automation Testing
```

#### What is Manual Testing?
Manual testing is the process of executing test cases manually without usirw automation tools to find
defects.

#### What is Automation Testing?
Automation testing uses tools and scripts to execute test cases automatically to improve efficiency and accuracy

#### Difference between Black Box, White Box & Grey Box Testing?
|Feature | Black Box Testing | White Box Testing | Grey Box Testing |
|---|---|---|---|---|
|**Code knowledge** | No knowledge of internal code | Full knowledge of code | Partial knowledge of code |
|**Tester** | Manual tester / QA | Developer / Automation tester | QA with technical knowledge |
|**Focus** | Functionality & UI | Code logic & structure | Functionality + logic |
|**Test case design** | Based on requirements | Based on code | Based on requirements & design |
|**Techniques used** | Equivalence partitioning, Boundary value analysis | Statement, branch, path coverage | Data flow, integration testing |
|**Access to source code** | ❌ No | ✅ Yes | ⚠️ Limited |
|**Example** | Login testing via UI | Testing if-else and loops | Testing UI + API + DB |

#### What is the Functional and Non-Functional Testing?
- **Functional Testing**\
  Functional testing ensures each feature works as according to requirements.\
  **Types of Functional Testing**

| Testing Type            | Description                                                          |
|:------------------------|:---------------------------------------------------------------------|
| **Unit Testing**        | Tests individual components or modules.                              |
| **Integration Testing** | Checks the quality interactions between integrated modules.          |
| **System Testing**      | Evaluates the system functionality as a whole.                       |
| **Acceptance Testing**  | Verifies that the system meets all business and end-user needs.      |
| **Regression Testing**  | Checks if any code changes break existing functionalities.           |
| **Smoke Testing**       | Quick checks to verify major functionalities after pushing new code. |

- **Non-Functional Testing**\
  Non-functional testing checks the **quality attributes** of the application.

| Testing Type              | Description                                                                           |
|:--------------------------|:--------------------------------------------------------------------------------------|
| **Performance Testing**   | Checks how fast and stable the application works.                                     |
| **Load Testing**          | Checks how the application works with expected number of users.                       |
| **Stress Testing**        | Checks the system behavior when the load goes **beyond the limit**.                   |
| **Security Testing**      | Checks whether the application is **safe from unauthorized access and attacks**.      |
| **Usability Testing**     | Checks how **easy and user-friendly** the application is.                             |
| **Compatibility Testing** | Checks if the system works equally well across different devices, browsers, and OSes. |
| **Recovery Testing**      | Verifies how the system recovers from crashes or failures.                            |



#### What is Bug, Error, Fault, Failure and Defect?

| Name        | Description                                                              |
|:------------|:-------------------------------------------------------------------------|
| **Bug**     | A mistake found during testing in the application.                       |
| **Error**   | A human mistake made by a developer or tester while coding or designing. |
| **Defect**  | When the software doesn't meet the expected requirement.                 |
| **Fault**   | An incorrect step or logic in the code that causes a defect.             |
| **Failure** | When the application stops working or behaves wrongly during execution.  |

> **Easy flow to remember**\
> Error &rarr; Fault &rarr; Defect &rarr; Failure &rarr; Bug
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
#### 
