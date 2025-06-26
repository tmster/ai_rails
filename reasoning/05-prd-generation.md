You are an experienced product manager tasked with creating a comprehensive product requirements document (PRD) based on the following descriptions:

<project_description>
{{project-description}} <- enter your MVP idea
</project_description>

<project_details>
{{project-details}} <- enter a summary of the planning session
</project_details>

Follow these steps to create a comprehensive and well-organized document:

1. Divide the PRD into the following sections:
   a. Project overview
   b. User problem
   c. Functional requirements
   d. Project boundaries
   e. User stories
   f. Success metrics

2. In each section, provide detailed and relevant information based on the project description and answers to clarifying questions. Make sure that:
   - You use clear and concise language
   - You provide specific details and data when necessary
   - You maintain consistency throughout the document
   - You address all points listed in each section

3. When creating user stories and acceptance criteria
   - List ALL necessary user stories, including basic, alternative, and edge cases.
   - Assign a unique requirement ID (e.g., US-001) to each user story for direct traceability.
   - Include at least one user story specifically for secure access or authentication if the application requires user identification or access restrictions.
   - Ensure that no potential user interaction has been omitted.
   - Ensure that each user story is testable.

Use the following structure for each user story:
- ID
- Title
- Description
- Acceptance criteria

4. Once the PRD is complete, review it against this checklist:
   - Can each user story be tested?
   - Are the acceptance criteria clear and specific?
   - Do we have enough user stories to build a fully functional application?
   - Have we included authentication and authorization requirements (if applicable)?

5. PRD formatting:
   - Keep formatting and numbering consistent.
   - Do not use bold formatting in markdown ( ** ).
   - List ALL user stories.
   - Format the PRD in correct markdown.

Prepare the PRD with the following structure:

```markdown
# Product Requirements Document (PRD) - {{app-name}}
## 1. Product Overview
## 2. User Problem
## 3. Functional Requirements
## 4. Product Boundaries
## 5. User Stories
## 6. Success Metrics
```

Remember to fill in each section with detailed, relevant information based on the project description and our clarifying questions. Make sure that the PRD is comprehensive, clear, and contains all the relevant information needed to continue working on the product.

The final result should consist solely of a PRD compliant with the specified format in markdown, which you will save in the .ai/prd.md file.

