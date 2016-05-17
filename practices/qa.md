## QA Guidelines

###What is Testing?
####Testing includes the following activities:
* Planning and control.
* Choosing test conditions.
* Designing and executing test cases.
* Checking results.
* Evaluating exit criteria.
* Reporting on the testing process and system under test.
* Finalizing or completing closure activities after a test phase has been completed.
* Reviewing documents (including source code).
* Conducting static analysis.

###Why is Testing necessary?
    Humans are fallible. We are prone to errors and we can be affected by time pressure, complex code, complex infrastructure, changing technologies, and/or many system interactions. So testing can have the following objectives:
        a. Finding defects.
        b. Gaining confidence about the level of quality of the product.
        c. Providing information for decision making.
        d. Preventing defects before the product is released for operational use.

    These objectives can change depending on the viewpoint why testing is done. For example:
        a. Development Testing (Component, Integration, System Testing)
            - Main objective may be to cause as many failures as possible so that they can be identified and fixed.
        b. Acceptance Testing
            - Main objective may be to confirm that system works as expected, to gain the confidence that it has met the requirements.
            - In some cases it may be just to assess the quality of the software (with no intention of fixing defects), to give information to stakeholders of the risk of releasing the system at a given time.
        c. Maintenance and Regression Testing.
            - This includes testing to ensure that no new defects have been introduced during development of changes.

###Seven Testing Principles
    These are general guidelines for testing.
        1. Testing shows presence of defects
            - Testing can show that defects are present, but cannot prove that there are no defects. Testing reduces the probability of undiscovered defects remaining in the software but, even if no defects are found, it is not a proof of correctness.
        2. Exhaustive testing is impossible.
            - Testing everything (all combinations of inputs and preconditions) is not feasible except for trivial cases. Instead of exhaustive testing, risk analysis and priorities should be used to focus testing efforts.
        3.  Early testing.
            - To find defects early, testing activities shall be started as early as possible in the software or system development life cycle, and shall be focused on defined objectives.
        4. Defect clustering.
            -  Testing effort shall be focused proportionally to the expected and later observed defect density of modules. A small number of modules usually contains most of the defects discovered during pre-release testing, or is responsible for most of the operational failures.
        5. Pesticide paradox.
            - If the same tests are repeated over and over again, eventually the same set of test cases will no longer find any new defects. To overcome this “pesticide paradox”, test cases need to be regularly reviewed and revised, and new and different tests need to be written to exercise different parts of the software or system to find potentially more defects.
        6. Testing is context dependent.
            - Testing is done differently in different contexts. For example, safety-critical software is tested differently from an e-commerce site.
        7. Absence-of-errors fallacy.
            - Finding and fixing defects does not help if the system built is unusable and does not fulfill the user's’ needs and expectations.

###Fundamental Test Process
    Test execution is the most visible part of testing. But to be effective and efficient, test plans should include time to be spent on planning the tests, designing test cases, preparing for execution and evaluation of results. The fundamental test process is consisted of the following main activities:
        a. Test planning and control.
        b. Test analysis and design.
        c. Test implementation and execution.
        d. Evaluating exit criteria and reporting.
        e. Test closure activities.
    Although logically sequential, the activities in the process may overlap or take place concurrently.
