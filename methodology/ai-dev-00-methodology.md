# AI Workflow for Development - Methodology

There are different development workflows for different types of projects. We consider using AI for:

- **New Application**: Creating a new application from scratch or modernizing an existing one.
- **New Functionality**: Adding new features, refactoring existing functionality, or fixing bugs in an existing application.

## Types of Development Workflows

### NEW APPLICATION:
1. Create a fully new application from scratch
2. Create a new application from an existing application, eg: modernizing an existing application, changing the technology stack, or migrating to a new framework.

### NEW FUNCTIONALITY:
1. Add a new feature into an existing application
2. Refactor of existing functionality
3. Fix bugs in an existing application

## CASE 1: AI Workflow for development of a New Application

The AI workflow for AI assisted development of a new application from scratch is divided into several steps:

1. **Create a detailed PRD**: The AI agent will assist the product manager in creating a detailed Product Requirements Document (PRD) for the new application. It will take an idea from the project and will conduct a questionaire to gather necessary information to create a comprehensive PRD.

The AI agent will compile its findings into a very extensive Markdown analysis document in the `PROJECT-ROOT-DIR/project-docs/` directory. 

`ai-dev-11-prd-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the project PRD `project-prd.md`.

⚠️ IMPORTANT: The human user must manually review, and optionaly improve iteratively with the help of an AI assistant before manually adding the PRD document to the project knowledge directory.

2. **Create an extensive Technical Analysis Document**: The AI agent will create a extensive technical analysis document.

`ai-dev-11-tech-analysis.md` - The AI agent (YOU) must follow the guidelines in this document to create the PRD `project-technical-analysis.md`

3. **Create an Implementation Plan**: The AI agent will create a detailed implementation plan with clear tasks broken down.

`ai-dev-20-implementation-plan-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the implementation plan `project-implementation-plan.md`.

4. **Execute the Implementation Plan to build each phase/epicfeature**: The AI agent will implement the tasks defined in the implementation plan for the specific feature.

The AI agent (YOU) must follow the guidelines in `project-implementation-plan.md` to implement one feature at a time, ensuring that each task is completed before moving on to the next one.


## CASE 2: AI Workflow for Development starting from an existing application

The AI workflow for AI assisted development starting from an existing application is divided into several steps:

1. **Explore the Codebase to create an Extensive Technical Analysis**: The AI agent will explore the entire code repository to understand the codebase from multiple perspectives: as a software architect, software developer, and product manager.

The AI agent will compile its findings into a very extensive Markdown analysis document in the root of the repository. This document will cover various aspects of the application, including architecture, features, design patterns, technology stack, user personas, and more.

⚠️ IMPORTANT: The human user must manually review, and optionaly improve iteratively with the help of an AI assistant before manually adding the `Technical Analysis` document to the project knowledge directory.

2. **Create a Product Requirements Document**: The AI agent will create a extensive product requirements document.

`ai-dev-prd-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the PRD `project-prd.md`.

3. **Create an Implementation Plan**: The AI agent will create a detailed implementation plan with clear tasks broken down.

`ai-dev-20-implementation-plan-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the implementation plan `project-implementation-plan.md`.

4. **Execute the Implementation Plan to build each phase/epicfeature**: The AI agent will implement the tasks defined in the implementation plan for the specific feature.

The AI agent (YOU) must follow the guidelines in `project-implementation-plan.md` to implement one feature at a time, ensuring that each task is completed before moving on to the next one.



## CASE 3: AI Workflow for adding a new feature to an existing application

[TODO:]

1. Create a new specific PRD for the feature based on the requirements of the new feature, and the analysis of the existing documentation for the application, which includes:
- `project-technical-analysis.md` - technical analysis of the application document
- `project-app-architecture.md` - application architecture document
- `project-technology-stack-and-project-structure.md` - Technology Stack and project structure document
- `project-implementation-plan.md` - Implementation plan document
- `project-prd.md` - Full application PRD document

`ai-dev-prd-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the PRD `project-prd-feature-XYZ`.

2. **Create an Implementation Plan for the new feature**: The AI agent will create a detailed implementation plan with clear tasks broken down for the new feature based on the requirements of the new feature, and the analysis of the existing documentation for the application, which includes:

- `project-technical-analysis.md` - technical analysis of the application document
- `project-app-architecture.md` - application architecture document
- `project-technology-stack-and-project-structure.md` - Technology Stack and project structure document
- `project-implementation-plan.md` - Implementation plan document
- `project-prd.md` - Full application PRD document
- `project-prd-feature-XYZ.md` - Feature specific PRD document

`ai-dev-20-implementation-plan-creation.md` - The AI agent (YOU) must follow the guidelines in this document to create the feature implementation plan `project-implementation-plan-feature-XYZ.md`.

3. **Execute the Implementation Plan to build each phase/epicfeature**: The AI agent will implement the tasks defined in the implementation plan for the specific feature.

The AI agent (YOU) must follow the guidelines in `project-implementation-plan-feature-XYZ.md` to implement one feature at a time, ensuring that each task is completed before moving on to the next one.

4. **Update the general documentation with the new changes and progress**: The AI agent will modify the current projecct documentation with the results of the newly implemented functionality.

[TODO:]
The AI agent (YOU) must follow the guidelines in `ai-dev-project-update-after-feature-XYZ.md` to modify the current project documentation.


---

