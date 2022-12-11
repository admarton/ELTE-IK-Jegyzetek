# Kutatásmódszertan Ea

# 3.EA 2022.09.28

## Laki Sándor

### Programmable network devices

- Unified interfaces for these devices
- Low level devices (switches) do computations

### Quality of service

- Resource sharing
- Scalability?
- Hardware is expensive, software is not scalable
- Programmable hardware can be the solution

## Data collection and analysis

- Peter Lehotay-Kéry
- Data from network devices
- Error detection for the future
- Compression of these data
- Heuristic error prediction
- Api for testing

## When we have the research theme and result

- How to write a article
- Scientific texts:
  - Research paper - **most important**
  - Report
    - Mainly for project founders
    - Overall picture for the project's results
    - Measurements, tests, long parts
    - For paid papers - altered report about the same for free
  - Survey paper
    - No new results
    - Collection of results
    - Good for us
  - Position paper
    - Wanted result is not available
    - What needs to be done to make the result possible
    - Where are we going
  - Letter
    - Short
    - 16th - 17th century result
    - Short answers for research papers, mistake corrections
  - Scientific book
    - Monographs
    - Lecture book alike
    - Researcher's all results of his field
    - 1 page ~ 1 day of work (only writing, not the result)
  - Book of proceedings, book of articles
  - PhD thesis, master theses
    - PhD ~ 3 results
- First things:
  - Abstracts and Discussion

### Scientific paper

- Result is the first
- IMRaD structure
  - Author with affiliation, ORCID
  - Title (unique)
  - Abstract (brief summary in IMRaD, few sentence, needs to be good)
  - Keywords, ACM classification
  - **Introduction**
    - Topic, question, goal, background, related works, state of the art
  - **Methods** (new)
  - **Results** and validation (new)
    - Better algorithm
    - New field
    - Validation should be reproducible
  - **Discussion**
    - IMRaD summary with new word, and things
  - Acknowledgement
    - Founders
    - Coworkers
  - Bibliography
  - Appendices

# 5.EA 2022.10.12

## Introduction

- Összefoglaló a state of the art-ról
- Hivatkozások a mondatokban
- Ki hivatkozott a cikkre -> újabb cikk ami hivatkozik
-

## Methods, Results

- Our solution, method and the results
- New algorithm
- Better algorithm
- Under certain conditions better
- Not better than every other solution in every condition
- Document the results
  - Algorithm
    - Szöveges leírás - textual
      - Hard to validate
      - Pongyola
    - Pseudocode
      - Algol like syntax
      - Cannot be real code
    - Flow-chart
    - Structogram
    - Validation
      - Prototype
      - Measurements
  - Protocol
    - Content and flow of messages
    - Sequence diagrams
    - Validation
      - Prototype, use-case
  - Architecture
    - Component diagrams
    - Not the task is the new
    - The architect type can be scientific
    - Validation
      - Use-case
  - Theoretical results
    - Definitions, lemmas, theorems, proof, formulae in structured order
    - Validation
      - Proofs are the validation
- Experiments, simulations, tests
  - Tables and charts - with captions
  - Focus on most significant results, do not include redundant data
  - Units, statistical notations
  - Appropriate type of chart
  - Axes, title, legends
  - Monochrome readability
    - Blue, red, black, if red not green
    - Dotted, stripped line

## Discussion, conclusion

- Question in the introduction (lot of interested people), promise
- We answered this question, goal achieved
  - Our answer is better than the existing ones
  - Can be shorter than the introduction
  - Compare results with related works
  - New research questions, further work
    - Promise to solve them soon

## Bibliography, references

- All the referenced papers, state of the art
- Style will define the references
  - [] before the dot.
  - `\cite`
  - Latex will convert it
  - `\documentclass(llncs)`
  - Bibtex records collected in bib files
    - only use the included records
    - BibTex record can be downloaded from the papers site
  - Collect cited items
  - make file:

```make
all:
pdflatex main.tex
bibtex main.aux
pdflatex main.tex
pdflatex main.tex
rm -f *.aux ...
clean: rm -f *.aux ...
```

# 6.EA 2022.10.19

## Acknowledgement

- For foundings
- `\thanks`
- Anonymous reviewer
- Anyone who helped
  - W programming
  - Administrators

### Appendices

- Complementary information

## Style of writing

- IMRaD structure
  - Sections, subsections
- Scientific writing in english
  - No synonyms
  - No ambiguity
  - No personal style
    - Wrong: I made...
    - Right: We made... (risky in thesis)
    - Passive (risky)
    - Combination in the same sentence is prohibited
  - No long sentences, with lot of parts
    - Short and clear
  - Abbreviations and acronyms
    - Introduce in the first use
    - Latin abbreviations should not be introduced
      - e.g. (for example), i.e. (in other words)
  - User is "he/she" or they, or passive
  - Numbers under 10 is spelled out
  - Number in the beginning of the sentence is spelled out

## Structure of presentation

- Conference presentation
- LATEXBeamer
- ~8 lines / slide
- No complete sentences
  - Keywords
  - Few word sentence
- IMRaD, title page, outline, numbers
- 15 minutes + 5 minutes Q&A
  - 1 minute / slide
  - Questions are good
    - Repeat the question
    - Try to answer - and ask if the answer was satisfying
- 20-40 words / slide
- Practice and measure time
- Figures
  - More data than words
  - Left size is the figure, right is the text
  - Caption
  - Few colors (4)
- Citation - name of the author
  - Should not use
  - Risky
- Additional slides for expected questions
- Formulas are hard to read and digest

## Conference

- Sessions (4-6 presentations), session chairs (he asks questions, keeps time limits)
- Time limits
- Training, trial talks
- All questions and remarks are important

# 7.EA 2022.10.26

Review process

## Peer Review

- Peer
  - PhD and PhD students can peer
- Peer scholars read and comment papers
- Quality assurance for the paper
- Journal specific criteria
- Other scientists accept the new result
- Output: errors, improvements, recommendations
  - Revision
  - Resubmission
- Acception rate
  - Target conference: one step above my level
- ISBN -> points
- One paper can be submitted to one journal
  - To submit again -> at least 30% difference
- Basic requirements:

  - Transparency, responsibility, accuracy, ethics

- Types
  - Preprint
    - no comments
    - only conference reviewers
    - Doubly blind review
    - Journal arranges the review
  - Pre-publication
    - modifications
    - Single blind review - reviewer knows the writer
    - Reviews are published
    - Third party arranges the review
  - Post-publication
    - Open - Writer and reviewer knows each other
    - Reviews are signed and published
    - Writer arranges the review

### Review forms

- Number of reviewers
  - 3-4 is the normal
- Reviewer recommendation for the journal:
  - strong reject
  - reject
  - weak reject
  - borderline
  - weak accept
  - accept
  - strong accept
- Summary of the Evaluation
  - Technical content
  - Significance of the work
  - Appropriate title, abstract, introduction, conclusion
  - Overall organization
  - Appropriateness for the conference ar journal
  - Style and clarity
  - Originality
- To declare novelty of the paper, reviewer should know the state of the art
- Appropriateness of methods, validation, references
- Comments on errors, typos, grammar, figures
- Proposal for improvements
- Reviewer's confidence - rate how confident the reviewer on that field

### Ethical issues

- Reviewer work for free
  - Voluntary reviewing
  - Lot of work
  - ORCID - number of reviews
- Cannot review if writer is
  - in the same institute
  - in the same research project
  - relative
- Check Plagiarism
- Review should write helpfully, realistically and respectfully

# 8.EA 2022.11.02

## EU Project Proposal

- Downloadable guide to write a project proposal
- Application form and Technical description
- Structure of the proposal
- Name and Acronym
- Form
  - Summary
  - List of beneficiaries
  - Budget breakdown
- Works
- Milestones
- Collaboration between researcher and industry partners
- Summary
  - Title
  - Start date
    - Found only from this date
  - Duration
  - Activity
  - Abstract
    - Length parameters
  - List of beneficiaries
    - Names, short names, country
    - Limits
  - Budget breakdown
    - Which partner, how much money
    - Research, Demonstration, Management(~10-15%), Other
    - Sum, Part of EU (max 75%)
- Work plan
  - Work packages
    - Like Project Management
    - Like Scientific Coordination
    - Title, Type, Lead beneficiary number (partner number), Person Month (time), Start, End
  - List of Deliverables (Work Package Tasks)
    - What the result will be
    - WP number, Leader, Person month, Nature(**R**esearch), Dissemination level, deliver time.
  - Work package description
    - All the prev infos
    - Objectives
      - List
    - Description and partner
    - Person month per participant
    - List of deliverables
    - Schedule of relevant Milestones
      - Number, name, leader, delivery date, comments
      - If milestones are not achieved, the EU can revoke money
  - All milestones
  - Tentative schedule of Project Reviews
    - This is when the EU checks in
      - They can stop the project
  - Tables with costs and work hours
- The scientific work
- **Gantt** chart
  - WP from when to when

# 9.EA 2022.11.09

## EU Project 2

- Description of Work
- Work packages, tasks, deliverable
- Project Description

## Project Description

- No details, prev stuff was detailed.

# 10.EA 2022.11.16

## Project Description - B part

- What is that we want to achieve

### Concepts and Objectives

- Introduction
- Challenge
  - What is the serious problem to solve
- Vision
  - 1
  - What we want to achieve
- Aims
  - 3-4
  - High level goals
- Objectives
  - 10-15 / aim
  - Work package
  - lower level goal

### Progress beyond the State-of-the-Art

- Methods
- New results promised
- List of Results beyond State-of-the-Art
  - Write what new result will be

### Success Criteria and Research Indications

- How to validate the results
- Hard criteria is hard to pass
- Low criteria is not good enough to win the project
- List of success criteria
  - Milestone criteria and end criteria
- Working software, benchmarks, validation methods

### S/T (Science/Tech) Methodology and Associated Work Plan

- Number of research papers published during the work.
- How many PhD students will be involved and graduated.
- Structure and dependency of work packages
- Objectives and corresponding WPs
- Risks and Contingency plans
  - Probability of missing objective by someone
  - What happens when someone cannot achieve something? How big is the problem?
  - Share the task between partners
- Timing and dependencies - Gant chart
  - Delay risk management - Max slack
- Critical path analysis

### Management Structure and Procedures

- Make it believable that we can accomplish what we promised.
- There is the management to manage the projects
- What are the risks? How are risks managed?
- Steering Committee
  - One person from every partner
    - Votes for big decisions
- Advisory Board
  - Professionals
  - Not stakeholder
- Work Package Team Leader
- Project Coordinator, Administrator - Project Management Expertise
- Beneficiaries - Principal Investigators
- Consortium as a whole
- Budget justification
- Management cost justification

### Beneficiaries

- Legit entities to create the results
- Pasts of the organizations

### Consortium as a Whole

- All of them required as a whole
- They complement each other

### Strategic Impact

- What happens when all of the objectives are completed
  - How it changes the world
  - The EU's software companies will create cheaper and better softwares than US or China
  - Greener computing

### Plans for the Use and Dissemination of Foreground Knowledge

- Ideas to share the new results
- Conferences, companies, people
- Marketing plan, business plan
- Company promise that they will sell more products and pay more tax based on the results than what the EU paid
- Who owns the money from the new results
- Intellectual property
- List of expected IP-s, protection, patents

# 11.EA 2022.11.23

- Not use the official forms, use the presentation as a base
