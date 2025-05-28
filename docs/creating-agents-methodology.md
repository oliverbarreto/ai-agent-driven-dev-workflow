# Methodology to create Agents

## 1. Define the Agent's Purpose
Clearly outline the specific tasks and responsibilities the agent will handle.

- agent_name: >
    Choose a descriptive and concise name for the agent that reflects its purpose.
- role: >
    Define the role of the agent in the context of the project or organization.
- goal: >
    Specify the primary goal or objective of the agent, including what it aims to achieve.
- backstory: >
    Provide a brief backstory or context for the agent, explaining its origin and relevance to the project. Defines the Persona.
- tools: >
    List the tools and resources the agent will use to perform its tasks effectively.

Example:
```yaml
chief_marketing_strategist:
  role: >
    Chief Marketing Strategist
  goal: >
    Synthesize amazing insights from product analysis to formulate incredible
    marketing strategies.
  backstory: >
    You are the Chief Marketing Strategist at a leading digital marketing agency,
    known for crafting bespoke strategies that drive success.
  tools: [search_tools, browser, calculator_tool, current_date_tool]
```

### Cheatsheet for defining the agents

Creating Agents Cheat Sheet:
- Think like a boss. Work backwards from the goal and think which employee you need to hire to get the job done.
- Define the Captain of the crew who orient the other agents towards the goal.
- Define which experts the captain needs to communicate with and delegate tasks to.
Build a top down structure of the crew.
Goal:

Captain/Manager/Boss:

Employees/Experts to hire:

Notes:
- Agents should be results driven and have a clear goal in mind
- Role is their job title
- Goals should actionable
- Backstory should be their resume

## 2. Design Agent's tasks
Define:
- task_name: Define a name for each task that is descriptive and concise
- description: >
    Provide a detailed description of the task, including its objectives and expected outcomes.
- expected_output: >
    Specify the format and content of the output that the agent should produce.

Example:
```yaml
research_task:
  description: >
    Conduct a thorough research about the customer and competitors in the context
    of {customer_domain}.
    Make sure you find any interesting and relevant information given the
    current year is 2024.
    We are working with them on the following project: {project_description}.
  expected_output: >
    A complete report on the customer and their customers and competitors,
    including their demographics, preferences, market positioning and audience engagement.
```

### Cheatsheet for defining tasks

Creating Tasks Cheat Sheet:
- Begin with the end in mind. Identify the specific outcome your tasks are aiming to achieve.
- Break down the outcome into actionable tasks, assigning each task to the appropriate agent.
- Ensure tasks are descriptive, providing clear instructions and expected deliverables.
Goal:
- Develop a detailed itinerary, including city selection, attractions, and practical travel advice.
Key Steps for Task Creation:
1. Identify the Desired Outcome: Define what success looks like for your project.
- A detailed 7 day travel itenerary.
2. Task Breakdown: Divide the goal into smaller, manageable tasks that agents can execute.
* - Itenerary Planning: develop a detailed plan for each day of the trip.
- City Selection: Analayze and pick the best cities to visit.
- Local Tour Guide: Find a local expert to provide insights and recommendations.
3. Assign Tasks to Agents: Match tasks with agents based on their roles and expertise.
4. Task Description Template:
- Use this template as a guide to define each task in your CrewAI application.
- This template helps ensure that each task is clearly defined, actionable, and aligned with the specific goals of

Template:
````
def [task_name](self, agent, [parameters]):
    return Task(description=dedent(f'"'
        **Task**: [Provide a concise name or summary of the task.]
        **Description**: [Detailed description of what the agent is expected to do, including actionable steps and expected outcomes. This should be clear and direct, outlining the specific actions requiired to complete the task.]
        **Parameters**:
        - [Parameter 1]: Description
        - [Parameter 2]: [Descristion]
        ... [Add more parameters as needed.]
        **Note**: [Optional section for incentives or encouragement for high-quality work. This can include tips, additional context, or motivations to encourage the agent deliver their best work, or also resources, or motivational messages to enhance the agent's performance.]
        '''), agent=agent)
```