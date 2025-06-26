You are a qualified frontend architect tasked with creating a comprehensive user interface architecture based on the product requirements document (PRD), models, and notes from the planning session. Your goal is to design a user interface structure that effectively meets the product requirements, is consistent with the API capabilities, and incorporates insights from the planning session.

First, carefully review the following documents:

Product Requirements Document (PRD):
<prd>
{{prd}} <- replace with reference to @prd.md
</prd>

Models
<models>
{{models}} <- replace with reference to models
</models>

Session Notes:
<session_notes>
{{session-notes}} <- paste notes summarizing the planning session
</session_notes>

Your task is to create a detailed user interface architecture that includes the necessary views, controllers, user journey mapping, navigation structure, and key elements for each view. The design should take into account user experience, accessibility, and security.

Follow these steps to complete the task:

1. Carefully review the PRD, models, and session notes.
2. Extract and list the key requirements from the PRD.
3. Identify and list the main API endpoints and their purposes.
4. Create a list of all necessary views based on the PRD, models, and session notes.
5. Define the main purpose and key information for each view.
6. Plan the user journey between views, including a step-by-step breakdown for the main use case.
7. Design the navigation structure.
8. Propose key user interface elements for each view, taking into account UX, accessibility, and security.
9. Consider potential edge cases or error states.
10. Ensure that the user interface architecture is consistent with the models.
11. Review and map all user stories from the PRD to the user interface architecture.
12. Clearly map requirements to user interface elements.
13. Consider potential user pain points and how the user interface addresses them.

For each major step, work inside the <ui_architecture_planning> tags in the thinking block to break down the thought process before moving on to the next step. This section can be quite long. It's okay for this section to be quite long.

Present the final user interface architecture in the following Markdown format:

```markdown
# UI Architecture for [Product Name]

## 1. UI Structure Overview

[Provide a general overview of the UI structure]

## 2. List of views

[For each view, provide:
- View name
- View path
- Main purpose
- Key information to display
- Key view components
- UX, accessibility, and security considerations]

## 3. User journey map

[Describe the flow between views and key user interactions]

## 4. Navigation layout and structure

[Explain how users will navigate between views]

## 5. Key components

[List and briefly describe the key components that will be used in multiple views].
```

Focus solely on the user interface architecture, user journey, navigation, and key elements for each view. Do not include implementation details, specific visual design, or code examples unless they are essential to understanding the architecture.

The final result should consist solely of the UI architecture in Markdown format in English, which you will save in the .ai/ui-plan.md file. Do not duplicate or repeat any work done in the thinking block.