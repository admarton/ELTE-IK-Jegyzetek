# Haladó szoftvertechnológia Ea

# 2022.09.22 EA 2

- Canvas fórumon lehet csapatokat szervezni

## What is a Software?

- Product? Service? Infrastructure?
- From products we go to services.
  - XAAS - X as a service
    - Infrastructure AAS
      - virtual computer
      - OS
    - Platform AAS
    - Software AAS
    - Function AAS
    - AI AAS
    - ... AAS
  - Version control AAS
    - GitHub, GitLab (open source)
      - Good for small solutions
      - GitHub -> have to pay for bigger projects
      - GitLab -> pay or self host
    - Why does GitLab works as a business?
      - If there is a problem or feature request
        - someone will pay for them to fix it
      - Open source code and service for more money
      - Infrastructure like the road system
        - Some people will contribute free
        - Some company will pay for things
        - Some company will give developers to keep up the infrastructure
        - Some people will pay for the service

## History of Product Handling

- Terracotta army - China
  - Body parts are made by different people
  - Assembled after
- Ford car factory - US
  - Factory
- Assembly line, Product line
- Separation and specialization for parts and people
- Mass production
- Interchangeable parts
- Predictability
- Phases
  - High quality - QA phase
- In the past software development started to become factory like

## System development Life Cycle

1. Initiation
2. System Concept Development
3. Planning
4. Requirement Analysis
5. Design
6. Development
7. Integration and Test
8. Implementation - Release, Setup
9. Operation and Maintenance
10. Disposition

## Testing

- Pyramid
  1. Unit test (largest)
  2. Integration test (medium)
  3. System test (few)
- White, gray, black box test
- Smoke tests
  - most important short tests
- Acceptance testing
  - contract based tests, fulfills requirements
- Regression testing
  - New features not break old ones
  - **If there is a problem -> write a test**
- Alpha/beta testing
- Usability/Accessibility testing
- Performance testing
- Destructive (Stress and Crash) testing
- Security testing
- A/B testing
  - Test A and B together and measure which is better

## WBS

- Work Breakdown Structure
  - Hierarchical structure
    - Children's scope adds up to parent's scope
  - Contains the whole Scope of the Project
  - Only tells scope, not schedule or detailed execution plan
  - Leaves can fit between two checkpoints
  - Break down until work unit
    - Can be reliable estimated
    - Is measurable
    - Fits the reporting period
- WBS top-down
  - It can be problematic
  - Different branch leafs can be solved in one
- Bottom-up can be better
  - find simplest / cheapest solutions
  - reuse existing technology and solutions
  - But functions can be forgotten
- Mix of both is the best
  - Create top-down (managers)
  - Then validate it (developers)

## Tools for WBS and beyond

- Trac
  - Version control, issue tracker, wiki
- GanttProject
  - Gantt diagrams
    - Time management
- Calligra Plan
  - Gantt diagrams
  - Order tasts to person
- LibrePlan
  - Charts
- Critical chain project management and critical path evaluation

## Other tools for projects

- Project execution - Kanban board
  - Notify other if you are late with the task
- Communication - Chat (spoiler alert: No)
  - Strict version control - good commit messages
  - Wiki - documentation
- Version Control - github, gitlab, gitea
- Build
- Testing Framework
- Deployment
  - DevOps

## SDLC Criticism - assembly line

- Good
  - Large projects, complex solutions
  - Detailed, well documented
  - Ease of maintenance
  - Can follow standards
- Bad
  - Time and Cost increased
  - Not flexible, cannot handle problems without full-design-first approach
- SSADM
  - Structured System Analysis andDesign Method
  - Standardization, factorization
  - Works well on similar problems/projects
  - Example: webshop developer company, digitalization of government infrastructures

# 3.EA 2022.09.29

## Developers are different

- Ninja
  - Few commits
  - Not much code
  - Solve problems with few lins
- Paraglider
  - Solve code
  - Not readable
- Cowboy
  - Not to much thinking
  - Starts coding immediately
  - Sometimes missis
  - Fast prototype
- Mage
  - Solve big problems
  - Scientist
  - Greek letter variables

## Problems are also different

- Trendy, design oriented web development company
  - Webshops
- Outsourcing company delivering information systems
  - Web UI
  - RestAPI
  - Databases
- Game developer company delivering on multiply platforms
  - Trendy games

## Important

- Know your
  - Team
    - Who does what
  - Task
    - What is the goal
  - Technology
    - Least important
  - --- In this order ---

## Cowboy coding or Code-and-fix

- Anti-pattern
  - Coding immediately
  - Bugs come, we fix them
  - Sometimes we test
  - Sometimes we release
- This pattern makes worse software

## Waterfall model

- Sequential
- Schedules and target dates
- Implement at once
- Tight control
- Document everything
- Big Design Up Front approach
  - From big picture to small details
- Different teams work on different steps
  - Managers make specification
  - Designers are sometimes programmers who thinks they are good architects
  - Maintenance team communicates with customers

### Good

- Predictable
- Robust

### Bad

- Slow and problematic
- Unable to react to changes

## V-Model

|                  |                   |                 |                |              |                     |
| ---------------- | ----------------- | --------------- | -------------- | ------------ | ------------------- | -------------- |
| Requirement anal |                   |                 |                |              |                     | System testing |
|                  | High level design |                 |                |              | Integration testing |
|                  |                   | Detailed design |                | Unit testing |
|                  |                   |                 | Implementation |              |                     |

- Slow
- Rigid
- Good quality software

## Prototyping

- Can try but not the best
- Good for handling uncertain parameters
- Try out different things - eg databases
- GUI mocks - client gives good feedback
- Types
  - Throwaway
  - Evolutionary (prototype becomes product)
  - Merging (or Incremental)
- Horizontal
  - GUI for the whole - but nothing works
- Vertical
  - One Button - all the functionality of the feature
- Fast, Cheap, Feedback
- No planning, Can be expensive with lot of iterations, developers dislike throwing away code

## RAD - Rapid Application Development

- GUI builders
- Simple apps can be made with editors
- Trendy project made easy

## Going Incremental

- Incremental waterfall
  - Small waterfalls
- Start with the most important independent feature
- Second feature can starts before the previous is finished
- The assembly line is in full capacity

## Spiral Model

- Waterfall + Prototyping + Incremental
- Parts
  1. Determine Goals
  2. Identify and resolve risks
  3. Development and testing
  4. Plan the next iteration
- Gets bigger in every circle
  - The product gets fuller
  - Has more and more features
- Flexible

## Chaos model

- Almost anti-pattern
- Lightweight model
- Easy for new developers
- Issue is the main part (Issue tracker)
  - Use this from the project start
  - Different types of issues
    - Priority
    - Value
    - Work type
  - Lifecycle
    - Bug:
      1. Unconfirmed
      2. New Bug - Duplicate
      3. Assign to someone
      4. Resolved
      5. Verified - Or reopened
      6. Closed
    - Lot of circles in the graph
- Bug Triage (From hospitals)
  - Collect information
  - Identify duplicates / similar problems
  - Filter
  - Set priority
  - Assign
  - Fast paced
  - Face to face
  - _This is the only rule in Chaos model_

# 5.EA 2022.10.13

- Canvas test
  - Not choice
  - Text tasks

## Agile (next)

- More freedom and more responsibility for team
- Flexible development
- Feedback loops are important
- People and interaction in the focus
- Working software and self documenting code

### Feature Driven Development

- Agile + MDD (Domain Object Modelling)
- Add new features to the existing product, safe
- Teams are temporal for features
  - Developer, ux, manager, tester
- Planning phase is long
  - UX is the most important
  - Cohesiveness
  - Models for the feature
  - Developers develop from the models
    - Class owner developer
- Releasable branches
  - Users cannot access new features
  - Business decision, AB testing
- Feature switch
  - Feature visibility can be turned on/off

### Scrum

- Teamwork, together strong
- Commitment
- Focus
  - Clear task
- Openness
  - Democratic
  - More info from the leaders
- Respect
  - Communicate with respect
  - Solve conflicts
- Courage
  - Tell if something is wrong
- Cross functional teams
- Decision making brought down
- Transparency
- Monitoring
- Steps:
  - Product Owner communicate with stakeholders
    - Which is the way
    - Creates Product Backlog
  - Product Backlog
    - Items
    - Stakeholders language
  - Sprint
    - Fixed length iterations
    - 2 weeks
      - 1 week is short for a working demo and presentation, retro and planning
      - 1 month is bad for the managers, few feedbacks
    - Something showable in the end
      - New feature
  - Developer team:
    - Sprint planning
      - Product Backlog -> Sprint Backlog
      - Task dependency
      - Sub tasks
      - Few hours
    - Daily Scrum / Standup
      - 10-15 minutes
      - What have been done - what will be done
      - Collect problems above the team, what prevents the team from work
        - Scrum master's task to solve these
          - Collaborate with other teams
    - Product backlog refinements
      - Sometimes priorities change
    - Sprint review meeting
      - 1 hour
      - 100% feature
      - Product Owner checks the new features
        - Feedback
    - Sprint Retrospective
      - 1 hour
      - Only the team
      - If there was a problem
        - prevent it from happening again
      - Make every sprint better
        - Productivity
        - Happiness
        - etc.
  - Scrum Master
    - Organize meetings
      - Sprint planning
      - Daily scrum
    - Solve problems
- PO, scrum master is not developer, not part of the team
  - Collision of interests
  - They have more teams
- Responsibility is on the team
- Meetings in person
- Triple constraint
  - Scope - Cost - Time o Quality
  - All of them cannot be fixed
    - Quality should be fixed
- Measure velocity
  - Burn down
    - Work to be done
    - Remaining tasks
    - ↓
  - Burn up
    - Work that is done
    - Fixed tasks
  - Size of the task is hard to measure
  - Who was productive in the team is hard to measure

### Kanban

- Billboard
- Minimize the waste
  - Toyota: Supply chain management
- Task is fixed
  - Need to do all of them
- Teams are fix, mostly
- Time is the variable
  - Checkpoints are important
    - But not determined by scope
    - Demo is not required for the checkpoint
- Teams pull tasks, not pushed from outside
- Work in progress limit

## Agile Thoughts

- Agile pyramid
  - Values, Principles, Methods
  - The values are the most important

# 6.EA 2022.10.20

## User Experience - User perspective

- Bonus points for real user for the MVP

- Customer or user
  - Is it the same?
  - If the user pays
    - more motivation for better ux
  - If its only business
    - Only try to sell the solution, ux is not in the focus
  - Few big or lot of small customers
  - If the customer is the user - the community is easier
- Early or late product launch
  - Early and half baked
    - Earlier rea user feedback
    - Competitors can copy it
      - Idea is not alone
        - Hard to copy with all the details
  - Late and better
    - Cost to laboratory testing
- Who will dominate the market
  - Apple is selling to users - UX dominant products
  - Microsoft is selling to big companies - UX is not that important

## UX

- UI is like a joke. If you have to explain, it is bad.
- Look, feel, usability
- - Visual design - look, feel
  - Structural design - usability
  - Interaction design - not statical, responsive
- How to measure user interactions
  - Which functions the use
  - How long does it take them
- UX practices
  - Customer feedback, user interviews
  - Labeled ratings - Rate our stuff 5 stars
    - Data scientist will know what is important
  - Survey
    - More feature idea than time to make is
    - Survey to choose whish is important
  - Problem sorting
  - Wireframing, GUI mockups
  - Personas
    - Users are different
    - User groups, stereotypes, personas
  - Scenarios
    - Functional requirements
    - Use cases
      - What they want
    - User stories
      - Why, how they want
      - How they know it
      - As a <type of user>, I want <some goal> so that <some reason>.
    - Storyboards
    - Simulations
  - Usability testing
  - A/B testing

### Lean UX

- Agile UX
- UX is important everywhere, from waterfall to agile
  - agile -> faster user feedback
- UX has to be cohesive
  - Teams have to work together

### Story driven modeling

- Steps
  - Draft scenarios
  - Mock-ups
  - Storyboarding
  - Class diagrams
  - Algorithm design
  - Implementation
  - Testing
- Can be waterfall or iterative

## DevOps

- Development - Testing - Operation
  - Conflicts
- Try to make them one group, to work together
- Hard to make in big teams
  - Cultural change

### DevOps Goals

- Improve
  - Time to market
  - Feedback loop delay
  - Commit to deploy
  - Quality
  - Efficiency
- Frequent release
- Automate as much as possible
- CI & CD

# 7.EA 2022.10.27

## Real users

- Count users
- API user limits

## DevOps

- Different functional teams have different needs and goals
- Put those different functional members in one team
  - Now they have a common goal
  - Its a cultural change
- Cost saving with automation of non creative tasks
  - There are lot of tasks which is not making the software
  - Try to automate those tasks
    - CI/CD

### VCS

- Code and review
- Organization
  - Centralized (Subversion)
    - Numbered versions
    - Trunc
    - Server holds the versions and the code
      - Developers only clients
      - They only get a part of the code and the history
      - Big load on server
  - Distributed (Git, Mercurial, Bazaar)
    - Hash for version
    - Main/master
    - Supports more users
    - Clients has the exact copy of the project
- Workflow
  - Branching
  - Merging (integrating)
  - Tags (Release)

#### Branching strategy

- Old school
  - Master
    - Always releasable / stable
  - Hotfix
  - Release branches
  - Development
    - Not always stable
  - Feature branches
    - New features
    - Bug fixes
- CI way
  - Master
    - Always releasable / stable
  - Feature branches
- Merging tools
  - Fork repository
    - Inherit feature branches
    - New custom feature branches
  - The main repo is developing
    - We can fetch from the main repo
  - Pull request / Merge request
    - I.e. GitHub, GitLab
    - Code review tool
    - If pass -> pull to the development

### Build, Test, Package

- CI Practices
  - Central Code Repo
    - Can be multiple
    - Not just geologically multiple
    - Different main repos for different solutions
      - Can be made if they are uniquely built and packaged
  - No binary in the repo
    - Especially auto generated stuff
  - Auto Build, Test
    - Sequence and hierarchy
      - Cost saving
  - Not much branches
    - Not too long living
    - Merge into main
  - Every commit should build and test
    - This can be time consuming
  - Artifact repository
    - Auto Built stuff
    - Logs - i.e. test logs
  - Show results with Dashboards
    - Good for the team and managers
- Jenkins
  - Open source
  - Old but gold
    - Plugin compatible
  - Dashboards
    - Status - Red,Yellow,Blue
      - Build failed, test failed, good
    - Weather
      - code coverage
      - performance tests
- "Earlier it is caught, cheaper to fix"
  - Code convention enforcement
    - clang-format, pep8
  - Testing frameworks
  - Build tools
    - CMake - development and build system independent
  - Build matrix
    - Different versions for the same products
      - Different target system, state
  - Code metrics, profiling
    - Sonar Cube - analysis
    - CodeChecker - static analysis
    - Jenkins - JaCoCo reports

### Release and Configure

- Manage infrastructure
  - Need more servers
    - Too much build tasks
    - Too much user
  - Deployment scalability - Virtualization
    - Full
      - Guest OS is as slow to boot as a real OS
      - We want fast boot and shutdown - on demand
      - Fixed resources
    - OS-Level - Containerization
      - Linux kernel
        - Containers use the same kernel
      - Fast boot and shut down
      - They separate the apps in the containers
      - Resource on demand
      - Resource allocation can be automated
        - Need more servers -> the are few new containers
  - Infrastructure as Code
    - Declarative configurations
    - Procedural
    - Pull or push

### Monitoring

- Performance monitoring
- General usage statistics
- Responsiveness
- Not profiling
  - That is slow
  - But module times can be measured
- Logging
  - ELK stack - elastic search - kibona

### Continuous Delivery

# 8.EA 2022.11.03

## OOP

- Why is it so important?
  - Its like our reality
  - Can beneficial for teamwork
- When to stop designing?
  - Design only the sprint's scope, but not ta make a hack, make a good logic
  - Hope for the best
- Examples:
  - Inheritance
  - Composition (Entity-Component system)
    - Can be better
- OOP Tools
  - Composition, inheritance
  - Delegation
    - Composite from what we would inherit, then delegate functions to that object
  - Polymorphism
    - Dynamic binding
    - Parametric
    - Template
    - Inheritance
    - Message passing
  - Goals
    - Reusability
    - Maintainability
    - Support team work
  - Tools are not enough
    - Good software needs good brains
    - Design patterns
    - Control flow vs data flow
      - Orthogonal things
      - Data flow in analytical software
    - Responsibility-driven design
      - What is responsible for what?
      - Put interactions in to interfaces
        - Client - server (can change)
    - Data-driven design
      - Design like a database
      - How to group data -> class
  - Unlimited ways of grouping, class making
    - Choose according to
      - SW process
      - Feature introduction - incremental

## SOLID

- S
  - Maybe separate
- O
  - Open for extension
  - Closed for modification
- L
  - Inherited object can be in a place of parent object
  - Upcast good, downcast no good
- I
  - Separate interfaces
  - Like scanner and printer is not always the same machine
- D
  - Coupling is not good
  - Higher abstraction should not couple with lower
    - If this is required introduce interfaces

## Architectural improvements

- Refactor
- Class normalization
- Design patters and anti patterns
  - Design patters are communication tools also

### Refactoring

- No change in functionality
  - But improve readability, simplicity, etc.
- Program transformation which not change outer behavior
  - Rename
  - Move
  - Break into components
  - Encapsulate
  - Generalize
    - Sonarqube
  - Branching into Compound State or Polymorphic behavior
    - Spaghetti code
      - Giant functions, lot of branches
    - Example - Deterministic definite state machine
      - Nested if-else
        - State is in the branches
      - Table of functions
        - State change rules in table
      - Inheritance
        - State is a object

### Class Normalization

- Like in database design
  - But not just data, functions also
- 1st object normal form (1ONF)
  - Iterative behavior
  - Change to a container
    - And its objects
- 2ONF
  - Helper function encapsulation
    - Shared behavior
- 3ONF
  - Class can be clastered
    - Few functions use few data
      - Class can be separated into few clasters

## OOA - Object Oriented Analysis

- Sketch up system, Implement, Improve
- Instead do deeply precise analysis
  - Design is so deep that become implementation
  - Shlaer-Mellor method + UML
    - = Executable UML
- Start with static parts
- Behavior is design with state machines
  - Methods that modify members
- Describe with action language
  - Read, write
  - Connection with other classes
    - Do something with them
- Simulation
- Test
- Compile to the desired language
- Example: Grippen factory uses this technique
  - trains, cars, cyber-physical modelling

## UML - Unified Modelling Language

- Communication tool mostly
- Class Diagram
  - Regular arrow
    - Pointer to the other object
    - If we manage the life it is aggregation or composition
- Component Diagram
  - Classes inside components
  - Interface --(O--
  - If they are loosely coupled with interfaces -> they can be components
- Deployment Diagram
  - Where are components running, how they communicate
- State Machine Diagram

# 9.EA 2022.11.10

- OOA order of UML diagrams

## UML

### 1. Use case diagram

- Who are the users?
- What they want and how?
- Only specification and design tool, not executable
  - If there are tons of usecases, we can separate then into parts/groups

### 2. Component Diagram

- Units of functionality and responsibility
- Interfaces
  - Executable requires good interface definitions
- Hierarchy diagram - sub components

### 3. Deployment diagram

- How to deploy those components
- Databases, servers, clients
- Used for localization
- Orthogonal to Class diagram

### 4. Class diagram

- Class structure of each component
  - Which not include any sub-component
- Classes are in the same memory space
  - Classes can have references to other classes
- Association names and multiplicity
- Arrow types
  - Association
  - Inheritance (Interface)
  - Dependency
  - Aggregation
  - Composition

### 5. Sequence diagrams

- Not part of the executable
  - Used for design and testing
- Objects, Communications
- Functions, workings
  - Parallel functions
  - Optional functions
  - Loops

### 6. State Machine diagram

- Enter state
- State changes, by events
- Sub-states
- Exit state
- Sequence diagram can be constructed from the state machines?
  - It should be!

### 7. Activity diagram

- Represent enter and exit state methods
- Not that useful, can become complicated

  - Changed to Action Languages
    - Like method bodies in a real programming language, but independent from the implementation

- Design not always come to this level
  - Options to generate codes from Component/Class diagrams
  - Implementation changes should be visible on the diagrams
  - Version control for UMLs

### UML criticism

- Good to visualize and present
- Nobody wants to program this way
- Easier to write than draw diagrams
- Diagrams can grow big and complex
  - If they not grow, then they are useless

### xtUML

- Executable
- Runs on a virtual machine
  - Debug the UML on that
- Model driven testing
  - Specification purpose of the diagrams
  - Test without real implementation

### Model Driven Development

- Use the above methods
- Model checking
  - Use model test to find invariants in the system
  - Check if invariants are true
  - As good as mathematic prove
    - Can be longer

## Design patters

- Best practice, good example
- Never code directly
- Common way of referring problems
- Naming conventions
- Communication tools
  - Easier to understand code
- Low-level patterns, but they can work in high-level

### Creational design patters

- Functions instead of constructors

- Singleton
  - Exists only one
  - Universally available
  - Only created if someone needs it
    - Lazy creation
  - Exists from then
  - In parallel systems all functions should be thread-safe
  - Test systems sometimes needs to create independent objects
- Factory method
  - Not construct different inherited classes
  - Different factories use different functions to construct inherited classes
  - Dependency injections
    - Inject the dependent inherited classes
  - Separate construction from the same business logic
- Abstract Factory
  - IE.: same logic on different platforms
- Prototype
  - Solve cloning problem
  - Create a new object based on an existing one
  - Hard to create the object
    - Lot of parameters
    - But there are few popular usecases
      - They get a prototype to create that object with the used parameters
  - Prototype registry
    - There are different prototypes which can be cloned
    - Search functionality
- Builder
  - Similar to prototype
  - Use the needed functions of the builder
- Lazy Initialization
  - Only construct the default stuff
  - The other things are constructed when they are needed
- Object Pool
  - Slow to create new object and destruct
  - Pool stores those objects and client can borrow them
- RAII
  - Exit scope is freeing resources

# 11.EA 2022.11.24

## Info

- 2 lectures left
- last week consultation
- Dec.19 Exam
  - 1 sentence question
  - Answers are not in the presentation
  - Canvas Quiz
  - Whole day - 10 minute
  - Canvas hard logging
- Dec.29 Last exam

## Design patterns

### Structural patterns

- Adapter
  - Adapt one system to another
- Facade
  - Create simpler interface to a complex system
  - Limitations for the facade's user
  - Multiple levels of facade for more options
- Proxy
  - Remote Method Invocation
    - Proxy to remote function
  - Protection
  - Caching
    - Store data
    - No database connection needed
  - From the outside everything is the same, but changes in the inside
- Bridge
  - Decuple abstraction and implementation
  - pimpl idiom
    - Pointer to implementation
- Composite
  - Tree representation
  - Leaf and composite nodes
- Decorator
  - Interface is same but inner structure can be different
  - Wrap inner parts and call inner functions
  - Decorator has the same interface
    - Adds new functionality to the methods, but also calls the inners function
    - Does both things
- Flyweight
  - Memory optimization
  - There are members that are the same in all the objects
    - Those can be in a singleton
- Mediator
  - Communication through the mediator
- Iterator
  - Iterate through a collection
- Visitor
- Chain responsibility
- Command
- State
- Memento

# 12.EA 2022.12.01

## Structural patterns

- Strategy
  - Pointer to a strategy
  - Different strategy implementation not interesting in executor
- Template Method
  - Steps in a method can be set as parameters
  - The function is the same, but some details can be changed

## Concurrency Design patterns

### Monitor Objects

- Mutual Exclusion
- Memory access, cache
- Spin-Lock
  - Low-level, os kernel
  - busy wait technique
  - ask and take resource
  - good for frequent changes
- Lock, wait
  - blocking while getting the lock
  - Busy waiting
- Condition variable
  - Like lock
  - condition + resource
  - blocking and non-blocking

### Active Objects

- Active when has it's own thread
- Decuple method execution from invocation
- Futures and promises
- Async invocation
  - Proxy
    - Ask to do something in the future
  - Scheduler
    - Do the asked thing
  - Variable with result or callback
    - Variable - Future
      - Is it ready?
      - If it's ready, you can get it.

### Reactor

- Read-write can be blocking
  - try to make it non blocking
- Multiple threads for read-writes
  - One thread blocks, the others can work
  - Not good for high number of connections
- OS level selective blocking
  - Ask if there is anything to read
    - If nothing then block everything
    - If there are few ready, execute those
- Event loop
  - Selective blocking
  - Sequential work on good resources
  - Dispatcher decides who works on the new resource
    - Finds handler
- Demultiplexes events synchronously
- Inverted control flow

## Architectural Design patterns

### Publish-Subscribe

- Event Bus
- Message queue
- Separate components can communicate with messages
- Decide who gets which messages
- Is it good?
  - Decoupling different parts, no references
  - Code reuse
  - Can become a monster

### MVC

- Model-View-Controller
- used for GUI
- Model
  - Data
  - State
- View
  - Show state
  - Reactive of fetching current state
- Controller
  - User uses this to change state

### PAC

- Presentation-Abstraction-Control
- P -> View, A -> Model, C -> C
- Multiple PAC in hierarch
  - Controllers can communicate with each other

### MVVM

- Model-View-ViewModel
- ViewModel - Controller/Mediator
- 3 tier

### Multitier

- n-tier
- above each other
- Only one up and one down communication

### Front controller

- Handle different tasks in different components
- Front decides which component is required for the task
- Entry-point

### SOA

- Service Oriented Architecture
- Micro services
- Independent parts in communication
  - Autonomous services
- Protocol for communication
- Find each other with a registry
- Should work without required connections
- Hierarchical services
- Implementation agnostic
  - Only interface matters
- Can become complex to maintain and test

### REST

- Representational State Transfer
- Best practices over HTTP
- Stateless operation
- Universal resource identifier
- Uniform interface
  - HTTP methods
  - JSON, XML, HTML.. output

### Service Locator

- Entities find each other

### Dependency injection

- Dependency can be changed of configured with input
- Framework can do this in the background

### IoC

- Inversion of Control
- Common thing calls for specific thing

### Microservices

- SOA + DevOps
- Full automation of tests and deployment
- Services should be small
- Automate fault tolerance and scalability
  - For horizontal scale is should be stateless

### P2P

- Peer-to-peer
- No client-server
- Distributed
  - Storage
    - Redundant parts
  - Search
    - Search in all nodes
  - Processing
    - parallel execution
- Routing and peer discovery
  - How to find each other
  - Hybrid solution - registry center

### MapReduce

- From functional world
  - Map - transformation on each
  - Reduce - many to one, aggregation
- Huge task
- Split the task
- Mapping, filtering, sorting
  - Transform data
- Shuffling
  - Group data from mapping by keys
- Reduce
  - Aggregate each group separately
- Final result
  - Collect all subtask's result
- Apache - ?HADU/ADU?, Spark
