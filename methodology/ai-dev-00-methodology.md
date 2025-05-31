# AI Workflow for Development - Methodology

There are different development workflows for different types of projects. We consider using AI for:

- **New Application**: Creating a new application from scratch or modernizing an existing one.
- **New Functionality**: Adding new features, refactoring existing functionality, or fixing bugs in an existing application.

## Types of Development Workflows

### NEW APPLICATION: (see cheat-sheet for details in `ai-dev-cheatsheet.md`)
1. Create a fully new application from scratch
2. Create a new application from an existing application, eg: modernizing an existing application, changing the technology stack, or migrating to a new framework.

### NEW FUNCTIONALITY:
1. Add a new feature into an existing application
2. Refactor of existing functionality
3. Fix bugs in an existing application


---


## CASE 1: AI Workflow for development of a New Application

The AI workflow for AI assisted development of a new application from scratch is divided into several steps:

1. **Create a detailed PRD**: The AI agent will assist the product manager in creating a detailed Product Requirements Document (PRD) for the new application. It will take an idea from the project and will conduct a questionaire to gather necessary information to create a comprehensive PRD.

The AI agent will compile its findings into a very extensive Markdown analysis document in the `PROJECT-ROOT-DIR/project-docs/` directory. 

`ai-dev-11-prd-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the project PRD `project-prd.md`.

⚠️ IMPORTANT: The human user must manually review, and optionaly improve iteratively with the help of an AI assistant before manually adding the PRD document to the project knowledge directory.

2. **Create an extensive Technical Analysis Document**: The AI agent will create a extensive technical analysis document.

`ai-dev-11-tech-analysis.md` - The AI agent (YOU) must follow the guidelines in this document to create the PRD `project-extensive-analysis.md`

Input documentation needed to create the implementation plan include:
- `project-prd.md` - Full application PRD document, the place where we describe the plan to create software ideas through structured and detailed sections

⚠️ IMPORTANT: After the AI agent has created the technical analysis document, the human user must manually review, and optionally improve iteratively with the help of an AI assistant before manually separating the `project-extensive-analysis.md` document into:
- `project-app-architecture.md` - an extensive application architecture document
- `project-techstack-projectstructure.md` - Technology Stack and project files structure document

The `Extensive Analysis` document (`project-extensive-analysis.md`) is also added to the project knowledge directory.

3. Continue with the AI Development with Memory Bank methodology to create an Implementation Plan, Context Scratchpad, and execute the tasks defined in the Implementation Plan described in detail in the section `## WORKFLOW FOR AI ASSISTED IMPLEMENTATION WITH MEMORY BANK METHODOLOGY` of this document. 

After it has finnised the implementation, it  also includes modifying the existing documentation with the results and knowledge acquired during the implementation of the newly implemented functionality, by updating the `project-implementation-plan.md`, `project-technical-analysis.md`, `project-app-architecture.md`, `project-techstack-projectstructure.md`, and `project-prd.md` documents with the new changes and progress made. It will also update `Known Issues` and `Lessons Learned` sections in the `project-implementation-plan.md` document.


---


## CASE 2: AI Workflow for Development starting from an existing application

The AI workflow for AI assisted development starting from an existing application is divided into several steps:

1. **Explore the Codebase to create an Extensive Technical Analysis**: The AI agent will explore the entire code repository to understand the codebase from multiple perspectives: as a software architect, software developer, and product manager.

The AI agent will compile its findings into a very extensive Markdown analysis document `project-extensive-analysis.md` in the root of the repository. This document will cover various aspects of the application, including architecture, features, design patterns, technology stack, user personas, and more.

⚠️ IMPORTANT: The human user must manually review, and optionaly improve iteratively with the help of an AI assistant before manually adding the Technical Analysis document (`project-extensive-analysis.md`) to the project knowledge directory.


2. **Manually Create a Product Requirements Document and Technical Documents**: 
 
⚠️ IMPORTANT: After the AI agent has created the analysis document of the previous step, the human user must manually review, and optionally improve iteratively with the help of an AI assistant before manually separating the `project-extensive-analysis.md` document into:
- `project-prd.md` - Full application PRD document, the place where we describe the plan to create software ideas through structured and detailed sections
- `project-app-architecture.md` - an extensive application architecture document
- `project-techstack-projectstructure.md` - Technology Stack and project files structure document

The `Extensive Analysis` document (`project-extensive-analysis.md`) is also added to the project knowledge directory.

3. Continue with the AI Development with Memory Bank methodology to create an Implementation Plan, Context Scratchpad, and execute the tasks defined in the Implementation Plan described in detail in the section `## WORKFLOW FOR AI ASSISTED IMPLEMENTATION WITH MEMORY BANK METHODOLOGY` of this document. 

After it has finnised the implementation, it also includes modifying the existing documentation with the results and knowledge acquired during the implementation of the newly implemented functionality, by updating the `project-implementation-plan.md`, `project-technical-analysis.md`, `project-app-architecture.md`, `project-techstack-projectstructure.md`, and `project-prd.md` documents with the new changes and progress made. It will also update `Known Issues` and `Lessons Learned` sections in the `project-implementation-plan.md` document.


---


## CASE 3: AI Workflow for adding a new feature to an existing application

1. **Create a new specific PRD for the new feature** based on the requirements of the new feature, and the analysis of the existing documentation for the application, which includes:
- `project-technical-analysis.md` - technical analysis of the application document
- `project-app-architecture.md` - application architecture document
- `project-techstack-projectstructure.md` - Technology Stack and project structure document
- `project-implementation-plan.md` - Implementation plan document
- `project-prd.md` - Full application PRD document

`ai-dev-11-prd-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the PRD `project-prd-feature-XYZ`.

2. Continue with the AI Development with Memory Bank methodology to create an Implementation Plan based on the new feature. Taking into account that this `project-prd-feature-XYZ.md` is a feature specific PRD document, so if needed, we must also take into account the whole project PRD Document, and the implications of the new feature in the existing application.

Therfore, we will create the Context Scratchpad, and execute the tasks defined in the Implementation Plan described in detail in the section `## WORKFLOW FOR AI ASSISTED IMPLEMENTATION WITH MEMORY BANK METHODOLOGY` of this document.

After it has finnised the implementation, it also includes modifying the existing documentation with the results and knowledge acquired during the implementation of the newly implemented functionality, by updating the `project-implementation-plan.md`, `project-technical-analysis.md`, `project-app-architecture.md`, `project-techstack-projectstructure.md`, and `project-prd.md` documents with the new changes and progress made. It will also update `Known Issues` and `Lessons Learned` sections in the `project-implementation-plan.md` document.


## WORKFLOW FOR AI ASSISTED IMPLEMENTATION WITH MEMORY BANK METHODOLOGY

3. **Create an Implementation Plan**: The AI agent will create a detailed implementation plan with clear tasks broken down.

`ai-dev-20-implementation-plan-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the implementation plan `project-implementation-plan.md`.

Input documentation needed to create the implementation plan include:
- `project-technical-analysis.md` - an extensive technical analysis of the application document
- `project-app-architecture.md` - an extensive application architecture document
- `project-techstack-projectstructure.md` - Technology Stack and project files structure document
- `project-prd.md` - Full application PRD document, the place where we describe the plan to create software ideas through structured and detailed sections

4. **Create a Context Scratchpad:** The AI agent will create a context scratchpad (`project-context-scratchpad.md`) from the `project-implementation-plan.md` that will be used to store the current focus of the context of the project and the implementation plan with the list of todo tasks, progress updates, and any relevant notes/issues/lessons learned.

5. **Execute the Implementation Plan to build each phase/epic/feature**: The AI agent will implement the tasks defined in the `project-context-scratchpad.md` for the specific feature/epic now being developed.

The AI agent (YOU) must follow the guidelines in the AI Development with Memory Bank methodology (`ai-dev-00-memory-bank.md`) to use the `project-context-scratchpad.md` to implement one feature/task at a time, ensuring that each task is completed before moving on to the next one.

6. **Update the general documentation with the new changes and progress:** The AI agent will modify the current project documentation (`project-implementation-plan.md`) with the results of the newly implemented functionality according to the guidelines in the AI Development with Memory Bank methodology (`ai-dev-00-memory-bank.md`) and the progress tracked on the `project-context-scratchpad`.

You will add he updated tasks to the project implementation plan, and will update, if needed, the `project-technical-analysis.md`, `project-app-architecture.md`, `project-techstack-projectstructure.md`, and `project-prd.md` documents with the new changes and progress made. It will also update `Known Issues` and `Lessons Learned` sections in the `project-implementation-plan.md` document.


---

