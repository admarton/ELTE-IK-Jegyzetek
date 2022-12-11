# Követelményelemzés EA

- Tanár: Kovács Attila
- Honlap: http://compalg.inf.elte.hu/~attila/Teaching.html
- Syllabus: http://compalg.inf.elte.hu/~attila/materials/RE_syllabus.pdf

Németh Gábor Árpád - másik tanár  
Bosch-tól is jönek majd  
16:00 kezdés

# 2. EA 2022.09.19

BOSCH-os csapat rendes problémán és rendes eszközökkel dolgoznak

Vizsga nyelve: írás - angol, szóbeli - magyar

- Projekt 30% - Írásbeli 70%
- canvas feleletválasztó rész
  - megajánlott jegy lehet
- ha nincs megajánlott akkor szóbeli

## Levels and types of Requirements

- Business level
  - Üzletszerű követelmények
  - Ez alatt lesz, hogy hogyan kell megvalósítani
  - Epic, bigger feature
  - Szöveges, ügyfél is megérti
- Stakeholder level
  - Igények
  - Részletek a szerplőknek megfelelően
  - Felhasználó is ide tartozik
  - Szabványok, szabályozások
- Product level
  - User Story
    - One day work for a developer
  - Functional requirement
  - Non functional
    - Performance, Reliability, Maintainability, Speed, Security
    - Not a function, but important
  - Data requirements
    - Structural and data complexity is equally important
    - What happens with the data and flow?
    - What will we do with the data?
  - External interfaces Req's
    - Connection with other softwares
    - Data flow between programs and libraries
  - Constraints
    - Example: the company only uses JAVA
- Transition level

## Layered Approach

- Requirements are decomposed, refined to smaller tasks
- Refinement for task and also for tests and documents
  - Know if it's good or not
  - Quality control

## RE Process and Related Activities

- **Why?** What?
- Not How?
- Technology independent
- Abstract requirements

## Types of product requirements

- Functional requirements
  - Functional requirements
    - Input - output
  - Behavioral requirements
    - State dependent output for the same input
  - Data requirements
- Non Functional requirements
  - Usually in natural language, related to functionality
- Constraint requirements
- Domain requirements
  - Additional req's
  - Added special knowledge (domain specific)
  - This is the hardest
  - Sometimes there are domain specific lows
  - Can differ or oppose with the other req's

## Non-functional req's

- Important to be able to test/verify/check these req's
  - Speed
    - Processed transactions/seconds
    - User/event response time
    - Screen refresh time
  - Size
  - Ease of use
    - Looks
    - Training time
  - Reliability
    - Mean time of failure
  - Robustness
  - Portability
- These can be opposing with each other
- What is the quality at a firm
  - Eg.: Performance or maintanablity is more important

## NRF Interaction

- Which is the **most critical** requirement?
- Spacecraft
  - Wight and needed fuel

## SW Product Quality

### ISO 9126

- Quality attributes
- Old

### **ISO 25010**

- 8 group of attributes
- Useful base for own requirements

### FURPS+ model

- Functional, Usability, Reliability, Performance
- Old
- - - Implementation

## Kano model

- Basic quality
  - This is the bare minimum for the product
- Expected quality
  - This is the normal
- Exciting quality
  - The COOL stuff
- All of that is important
- With time the requirements move
  - The Exciting stuff becomes the normal - exciting -> delighter
  - The normal becomes the minimum - expected -> satisfier
  - The minimum is not enough - basic -> dissatisfier
- Calculate with the future
  - Exciting is needed all the time to get users

## Requirements Engineering Activities

- Inception
  - things before planning
  - what is possible and what is not
  - if something is not working -> why -> now what
- Development
  - What to make?
  - Elicitation - feltárás
  - Analysis - elemzés
  - Specification - dokumentálás
  - Validation - ellenőrzés
- Management
  - Change in requirements
  - Long term management

## The need of a Glossary

- We need to use the same words for the same things
- Same language is required
- Tip: Use a glossary - download one and edit if its needed
- Glossary management is different

## Key Concepts

- The ability to **Elicit** the requirements from users is crucial

# 3.EA 2022.10.03

- Gábor Árpád Németh
- From the brainstorming to the prototype

## Green field projects

1. Initial thoughts - Brainstorming
   - What to achieve
   - Scope
   - Possible customers
   - Budget
2. Refine requirements
   - Too general
     - Massive architecture
     - Features that nobody uses
   - Too specific
     - Hard to extend
     - Hard to maintain
     - Not future-proof
   - Possible customers' problems, goals, workflows
3. Create a prototype
   - Proof of concept
   - What would like to achieve?
     - List of functions
   - How we want to achieve?
     - UI
     - Who will use? Knowledge?
     - Performace
     - Workload
     - Scalability
     - How to handle overload?
     - Software <-> Hardware
     - Security
   - How we should provide expected quality?
     - Manual testing
     - Automatic tests on prototype
     - Proof of concept tests
   - Not implementation
   - Most prototypes not become product
     - Wrong assumptions
       - Requirements, scope
       - Customers and needs
       - Budget
     - Change in company - cost cut / project closure
     - Similar product has been developed
   - If prototype is good:
4. Productification
   - Reviews
     - Architecture
     - Management

| \_       | Project                        | Product                       |
| -------- | ------------------------------ | ----------------------------- |
| Generic  | Unique, customer specific      | Generic                       |
| Time     | Beginning and end date         | Permanent                     |
| Planning | One step / Predictive planning | Iterative / adaptive planning |
| Input    | Project requirement            | Evolving                      |

# 6.EA 2022.10.17

- Nov.21 Monday is the due date for the homework

## Brown field projects

- Change request
- Early estimate
- Task clarification -> feature specification
- Design documents
- Implementation
- Tests
- Documentation
- Deployment

### Customer requests a change

- Describes what they want
- Not a detailed description
- Client perspective
- Ambiguous, inconsistent

### Early estimation

- Limited time and effort
  - Not perfect estimation
- Output is a overview of the topic, affected parts, possible bigger tasks
  - Polo size
    - S - 0-40 mhrs (man hours)
    - M - 41-80 mhrs
    - L - 81-200 mhrs
    - XL - 200+
    - Just a example
      - Different teams has different polo sizes
      - Max 1 size error

### Task clarification with customer

- Iterative process
- Needs to be transparent
  - Update in CR management system
    - New people can catch up with the project
- Check related standards
  - Deviation from the standards should be documented
- Check related existing features
  - Already exists
  - Compatibility
  - Backward compatibility
- Output: Feature Specification

  - Required functionalities
  - Developers, testers and technical writers can use it
  - Use case - user story
  - Use case
    - Described as Precondition, Actions, Post condition
  - User story
    - Which type of user
    - What he wants
    - How
  - References, standards, keywords
  - Risks about the feature
  - Test design
  - Scope
  - Glossary, Shorts
  - Existing use-case impacts
  - Pre - post condition
  - Normal flow - alternate flow
  - Exception flow
  - System impact
  - Test analysis
  - Non functional
    - Capacity, performance
    - Customer impact
    - Backward compatibility

- Feature Specification must be accepted by both sides

  - Business analyst, developer, tester
  - Review responsible
    - Screening
    - Moderate review, give verdict (accept, accept w comments, reject)
    - Check afterlife based on verdict (check modifications to comments, new turn in review)
    - Update status on CR management system
  - Customer review

- Risks
  - We want that feature right now!
    - Hard to generalize and maintaine solution
  - Too big requirements
    - Never finished
  - Requirements not conform with standards
    - Compatibility problems later
  - Problem with documentation
    - Misunderstandings, conflicts
    - Changes must be documented (delays, cost)
  - Document delivered feature
    - Design decisions
    - Prevent reverse engineering
      - Approve with the customer
        - Additional cost, loss of credibility
  - ## No traceability

# 11.EA 2022.11.21

- Exam

  - Canvas big exam or lot of small exams (20 people / exam)
  - Preferred: english, canvas
  - Canvas: Single choice questions, no negative points
  - When:
    - Dec. 21 - 16:00
    - Jan. 05 - 16:00
    - ...
  - Tips:
    - UML, SysML - should know from BSc

- Requirements are important for IT

## Requirements Elicitation

- Discover the product level requirements
  - Customer don't know how he wants what he wants

### Elicitation Techniques

- Available time
- Money
- Knowledge
- Types
  - Survey
    - Interview
      - Face to face
      - 1 or 2 customer
        - If there are more people, there wil be a hierarchy within
          - The underdog won't tell the truth
      - Discussion about what he wants
      - Competent person is required
      - His word cannot be overridden
      - Prepare with some questions
        - Get his opinion
        - Sometimes the first question can make the others useless
      - Questions are flexible and personal
      - Don't make to long
        - They get exhausted
        - Max 1 hour, preferably less
      - Take notes
        - Precise notes
        - During and after
        - What is not written, that not exists
    - Questionnaire
      - Some questions
      - Force my view on the customers
        - Not flexible or personal
      - Lot of people can be questioned
      - Everything is written
      - Don't make too long (5-10-15 mins)
      - Short questions, require short answers
  - Creative techniques
    - Brainstorming
      - Any idea is a good idea
      - After we need to filter them
      - Good for small teams
      - Short meetings
      - Good for revolutionary requirements
        - Why users will choose my product
    - 6-3-5 Brainwriting
      - Clearer ans structural
      - 6 person, 3 idea, in 5 minutes
      - One after another
      - Not require a moderator
      - Everyone is active and should improve previous ideas
      - No premature discussions
      - Hard describe idea in short format
      - Time limit can be a pressure
    - Brainstorming paradox
      - Negate everything
      - How could be bad
      - Negate everything -> requirements
      - How to make in not work
      - Can be beneficial sometimes
    - Change of perspective (6 thinking hats)
      - See fom 6 perspective
        - Everyone should see the problem on that perspective
        - Can avoid internal conflicts
      - White hat
        - Analytics
        - Data
      - Red hat
        - Feelings
      - Black hat
        - Cautious
      - Yellow hat
        - Bright
      - Green hat
        - Creative
      - Blue hat
        - Manage all the hats and ideas
      - There are two types of managers
        - Dreamworld -> gives vision
        - Engineer -> keeps reality
    - Analogy technique
      - Analogy form history, biology and life
      - What would happens if this were that
      - Copy good things
  - Document-centric techniques
    - System archeology - legacy, competitors
    - Perspective-based reading
      - IE.: management, engineer, economics, developer, qa perspective
    - Reuse
      - Not just copy paste
      - Libs, functions, components
      - If something is good, reuse it.
        - Don't invent the wheel every time
  - Observation techniques
    - Process observation
      - How now works
      - How can it ba as good but better
    - Apprenticing
      - Question how those things work
      - Make requirements from them
  - Support techniques
    - Mind map
    - Prototype
    - Workshop
    - CRC Cards
    - Use case modelling
      - How processes work

### Guidelines

- Feasibility
- Organization political consideration
- Record requirement sources
- Identify and consult stakeholders
- Use appropriate techniques
- Multiple viewpoints
- Prototype
- Look for Domain constraint
  - They think their are trivial
- Reuse requirements

### Analysis and negotiation

- Requirements analysis
  - Priority
  - Refinimg
- Managing complexity
  - Cannot create product with too much requirements
    - 25 - 100 features in one project
    - If more than 50 separate into more projects
  - Small, managable inforamtions
  - Attributs of a feature
    - Status
    - Benefit - Important-Satisfier
    - Cost & effort - man-hours, function-points
    - Risk - High-medium-low
    - Stability - probability of the feature will change
    - Target release
    - Target Iteration
    - Assigned to
    - Reason - Tracebility
    - Priority

# 12.EA 2022.11.28

- Should read the book on the lecture's website

## Quality criteria

- Agreed - everyone accepts
- Ranked - importance, priority
- Unambiguous - for non-formal and half formal models
- Valid and up-to-date
- Correct - idea of stakeholders
- Consistent - ellentmondásmentes
- Verifiable - Have to measurable
- Realizable - possible to implement
- Traceable - Who sad that, who will use it
- Complete - Which depth is good
  - Not to refined, but all parts that are necessary
- Understandable - Short, not a poem

## Interactions

- How requirements are connected
- There can be controversies, should eliminate them
  - One or two architect knows the whole system
  - Every change should be approved by them
    - cuz they know if anything breaks with those changes

## Requirements Documentation

- What is not written, that doesn't exists
- Three perspectives
  - Data
    - Static structural date
    - Like class diagrams
    - There is static and dynamic
      - Static is like data in the database
      - Dynamic is how data flows through the system
        - ie.: how much and how frequent
  - Functional
    - How to handle that data
    - Input-output is always the same
  - Behavioral
    - Output depends on state
    - State machine

## SysML

- Graphical model for the software and hardware
- Use some UMLs and new charts like requirements
- Requirement Diagram

## Document models

- Natural language
  - Understandable
  - May be ambiguous
  - Perspective can be mixed
  - Sentence template for better understandability
- Conceptual model
  - Modelling languages
  - One perspective
  - Requires special knowledge
- Hybrid model
  - Natural language for stakeholders
  - Model for developers and engineers

## SRS - System Requirement Specification

- Base of a contract
- IEEE 830 Standard template
- Code is not requirement
- Intro
  - Glossary
  - System overview
  - References
- etc

## Good requirement

- What not How
  - Not implementation dependent
- Unique identifier
  - Symbolic identifier - few characters
- Short sentences
- One sentence per requirement
- Use limited vocab
- Don't use requirements with
  - conjunctions: and, or, etc
  - phrases: if, etc
- Use positive sentences
  - Passive and negative is not good
- Avoid wishfulness
  - Danger words: usually, often, probably, all platforms, never fail

## Requirements have attributes

- Dates
- Version
- Status
- etc

## Requirements validation

- Inputs
  - Times, prices
- Output
  - Problems
  - Agreed actions
- Are the requirements correct
- Are they written correct
- Are they clear and refined enough
- Involve the correct stakeholders
  - Engineer
  - Document expert
  - Decision maker
- Do not correct - just show the mistake
- Change in documentation type
  - Non-formal <-> Semi-formal
- Repeated validation
- Reviews, Prototypes, Model validation, checklist

## Requirements Management

- Baseline is cerated, now managements starts
- How to implement changes
  - Deletion is easy
  - How new requirements impact the system
- Important to see the impacted requirements
- Do not work on obsolete requirements
- How much the new requirements cost
- Managements
  - Change control
    - Not just put in
    - Every important person should agree on it
      - Change Control/Advisory Board
    - Should it be implemented
    - When should it be implemented
  - Version control
  - Requirements status tracking
    - Up to date with the status
  - Requirements tracing
    - Chains of why and what
- Metrics and views
  - Clear, understandable, valid and reproducible
  - Requirement status vs plan
  - Requirements volatility
  - External Interface Status vs Plan
- Views

  - Selective
  - Condensed

- Time estimation tools
  - Works good on big projects
  - CoCoMo - Constructive Cost Model
- Work with less errors
  - PSP - Personal Software Process
    - Collect typical mistakes

## Tools

- What is the best for your project

## Sentence template

1. Where, under what condition
2. THE SYSTEM
3. shall, should, will
4. PROCESS, ...
