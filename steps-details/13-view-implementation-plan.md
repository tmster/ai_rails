# Rails View Implementation Plan Generator

As a senior Rails developer, your task is to create a detailed implementation plan for a new view in a Rails application. The plan should be comprehensive and clear enough for another developer to correctly implement the view and related components.

First, review the following information:

1. Product Requirements Document (PRD):
<prd>
{{prd}} <- reference to @prd.md file
</prd>

2. View Description:
<view_description>
{{view-description}} <- paste view implementation description from ui-plan.md
</view_description>

3. User Stories:
<user_stories>
{{user-stories}} <- paste user stories from @prd.md that will be addressed by the view
</user_stories>

4. Tech Stack:
<tech_stack>
{{tech-stack}} <- reference to @tech-stack.md
</tech_stack>

5. Models:
<models>
{{models}} <- paste relevant model definitions
</models>

## Implementation Analysis Requirements

1. For each input section (PRD, User Stories, Tech Stack):
   - Summarize key points
   - List requirements/constraints
   - Note potential challenges

2. Extract key requirements including:
   - Database schema needs
   - Model relationships
   - Controller actions
   - View templates
   - Helper methods
   - Mailers (if needed)
   - Background jobs (if needed)
   - API endpoints (if needed)

3. Component Planning:
   - Required controllers with actions
   - View templates and partials
   - Helper modules
   - JavaScript/Stimulus controllers
   - Required gems
   - Testing strategy

4. Data Flow Analysis:
   - Model interactions
   - Controller-view data flow
   - Form handling
   - API integrations
   - Real-time updates (if using Turbo)

## Deliverable Format

Provide implementation plan in Markdown with these sections:

1. Overview
   - View purpose
   - Key features
   - Technical approach

2. Routes
   - Route definitions
   - Required namespaces
   - RESTful/custom actions

3. Models
   - Schema updates
   - Associations
   - Validations
   - Scopes
   - Callbacks

4. Controllers
   - Controller class definition
   - Required actions
   - Before/after filters
   - Strong parameters
   - Error handling

5. Views
   - Template hierarchy
   - Partial structure
   - Form builders
   - Helper methods
   - Turbo Frames/Streams usage

6. Components (if using ViewComponents)
   - Component hierarchy
   - Props/parameters
   - Templates
   - Preview examples

7. JavaScript
   - Stimulus controllers
   - Custom modules
   - Third-party integrations

8. Testing Plan
   - Model specs
   - Controller specs
   - View specs
   - System tests
   - API tests

9. Implementation Steps
   - Ordered list of tasks
   - Dependencies
   - Testing checkpoints

10. Error Handling
    - Validation errors
    - Edge cases
    - Error pages
    - Logging strategy

Output should be saved in `.ai/{resource_name}-implementation-plan.md`

Example output structure:

```markdown
# User Dashboard Implementation Plan

## 1. Overview
[Description of the dashboard view and features]

## 2. Routes
```ruby
# config/routes.rb
resources :dashboard, only: [:index, :show]
```

## 3. Models
[Model definitions and relationships]

## 4. Controllers
[Controller implementations]

## 5. Views
[View template structure]

# [Continue with other sections...]
```
