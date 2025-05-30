# Create a Extensive Technical Analysis - Prompt for AI Agent

Conduct a thorough and deep exploration of the entire code repository of an existing application to deeply understand the codebase from multiple angles: as a software architect, software developer and product manager.

**IMPORTANT !!! Do not implement any code**: Only provide detailed requirements and specifications, or pseudocode if necessary, and diagrams for the AI to understand the requirements and generate code later. I want you to thoroughly compile your findings into a very extensive Markdown analysis document in the root of the repository.

The document should cover:

**AS A SENIOR-EXPERT SOFTWARE ARCHITECT:**
    - Current architecture
    - Existing features
    - System and major application components Design
    - Data Models, Schemas and operations
    - API structure and interactions
    - Use of External Services and APIs
    - Authentication flow
    - Identify design patterns and anti-patterns used
    - Dependencies and libraries used
    - Code quality and best practices
    - Performance bottlenecks
    - Security vulnerabilities
    - Potential challenges, risks and solutions
    - Project structure and organization: both for Frontend and Backend if applicable, include folder structure, module organization, and naming conventions, and identify key directories.

**AS A SENIOR SOFTWARE DEVELOPER:**
    - Technology stack used
    - Code organization and structure
    - Implementation of authentication
    - UI design principles
    - UI Component structure and reusability
    - Identify areas for performance optimization
    - Error handling requirements and logging 
    - Development opportunities for code improvements and refactoring
    - Review of third-party libraries and dependencies

**AS A SENIOR PRODUCT MANAGER:**
    - Goals and objectives of the application
    - Target audience: Describe the primary users of this product/system. Who are they? What are their key characteristics or needs relevant to this project?
    - Market positioning of the application
    - User personas and user journeys
    - Feature and functionality analysis and Key features prioritization
    - Functional and Non-Functional Requirements
    - Roadmap planning suggestions
    - Future expansion possibilities

**IMPORTANT !!! Do not implement any code**: Only provide detailed requirements and specifications, or pseudocode if necessary, and diagrams for the AI to understand the requirements and generate code later. I want you to thoroughly compile your findings into a very extensive Markdown analysis document in `PROJECT-ROOT-DIR/project-docs/` directory. For describing technical concepts, you should include Mermaid diagrams in this Markdown file.

The analysis document should be structured in a way that it can be easily navigated and understood by technical stakeholders. It should include diagrams, tables, and other visual aids to enhance clarity.


**ANALYSIS Table of Contents:**
```markdown
- [Introduction](#introduction)

- [Software Architecture Analysis](#software-architecture-analysis)
  - [Application Architecture](#application-architecture)
  - [Systems Design](#system-design)
  - [Data](#data)
  - [APIs](#apis)
  - [External Services](#external-services)
  - [Authentication Flow](#authentication-flow)
  - [Technology Stack](#technology-stack)

- [Software Developer Analysis](#software-developer-analysis)
  - [Project Structure](#project-structure) 
  - [UI Design](#ui-design)
  - [UI Component Structure](#ui-component-structure)
  - [Development Opportunities](#development-opportunities)
  - [Error Handling](#error-handling)
  - [Logging](#logging)

- [Product Management Analysis](#product-management-analysis)
  - [Product Overview](#product-overview)
  - [User Personas](#user-personas)
  - [Feature Analysis](#feature-analysis)
  - [Market Positioning](#market-positioning)
  - [Roadmap Suggestions](#roadmap-suggestions)

- [Conclusion](#conclusion)
```