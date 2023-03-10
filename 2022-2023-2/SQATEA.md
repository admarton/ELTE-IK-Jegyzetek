# Software quality and testing

# Lecture 1

- 16:00 start
- About methodology
- How can you work as a Testing Manager?
- Exam like ISTQB foundation level test

## Content

- Basic terminology
- Project lifecycle
- Test levels
- Testing lifecycle
- Design techniques
- Implementation and execution
- Documentation
- Monitor
- Management
- Automation

## Books

- Foundations of software testing
- The Software Test Engineer's Handbook
- Practical Test Design
- Detect Almost all the bugs

## Exam

- Writen test
- Selection questions, 1 good in 4
- 26 point - grade 3

## Why we test?

- Auto tests require developers
- We are unable to prove industry level code
- Use testing to try requirements

## Definitions

- Error / mistake
    - mistake by people
- Fault / defect / bug
    - result of an error, mistake
- Failure
    - Occures when fault executes
    - Faults can hide for years
- Incident
    - Symptom of a failure
- Root Cause
    - Sometimes we do not want to find it, just cure the symptoms
- Verification
    - Am I building the product right?
- Validation
    - Am I building the right product?
- Quality
    - Hard to understand
    - Depends on the customer

Testing just controls quality, not improves it!

## Levels

- Testing - This is the course material
- Quality Control
- Quality Assurance

## Quality factors

- Testability
- Maintainability
- Modularity
- Reliability
- Efficiency
- Usability
- Reusability
- Legal requirements / standards
- etc.

## Cost & Quality Iceberg

- Above the water is what the users see
    - Features
    - UI
- Others are not intrested
    - Code quality
    - design
- There are hidden costs for things

# 2. EA

## Typical objectives of testing

- evaluate work
- verify, validate
- etc.

## Testing is hard

- We cannot test all the paths that a code can execute
- P - program
- D - domain
- test data - t - t in D
- test data set - T - T subset of D
- More tests are not neccessary better
- The test set should be efficient
- Why
    - Time and budget problems
        - It is the last step
    - Lack of knowledge
        - Not all universities teach testing
    - Diversity of enviroments
    - Increasing complexity
    - Devs are not trained of motivated to test
    - Testers are willing but incapable
    - Lack of culture

## Why deffects occur

- People are not perfect
- Poor communication
- No clear requirements
- Changing requirements
- Assumptions

## Cost

- Can cost a lot
- Space projects
- UK tax refund system
- Can cost LIVES
- Earlier we find the bug the cheaper it is.
    - Shift left strategy

## Techniques

- Static
- Dynamic
    - Structural
        - Data Flow
        - Control Flow
    - Behavioral
        - Functional
        - Non-functional

## Bugs classification

- Nature
    - Functional
    - Performance
    - Usability
    - Security
    - etc.
- Severity
- Priority
- Detection difficulty
    - First order bug
        - single parameter triggers it
        - easy to localize the root cause
    - Higher order bugs
        - more params need to align to cause the bug

## Test selection, adequacy

- Which test cases should be selected?
- Was test suite good enought?

## Coverage

- Is not about quality
- Untested parts not functionality
- More types of coverage
    - requirements
    - structural
    - architectural

## Fault localization

- Where is the root cause?
- Bigger test cases
    - If they fail, then run the finer tests
        - In the end single fault assumption

## Principles

- Testing is possible
    - Competent Programer Hypothesis
        - Developers wants to create good code
    - C Tester H
        - Exhaustive testing is impossible
- Testing should start as soon as possible
    - Testing sould begin in the requirement review phase
- Testing and development should be independent
- Testing is context dependent
    - Everithing is different from project to project
- CD requires continous testing
    - new code require new tests

