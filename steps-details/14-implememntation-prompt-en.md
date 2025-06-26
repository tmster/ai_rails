# Rails Invitation Confirmation Implementation Plan

This implementation plan outlines the steps to create a fully fun### 4. Component Implementation
```ruby
# app/components/confirmation/card_component.rb
class Confirmation::CardComponent < RubyUI::BaseComponent
  def initialize(invitation:)
    @invitation = invitation
  end

  private

  def template
    div(class: "rounded-lg shadow-sm p-6") do
      # Implementation
    end
  end
end
```
- Create RubyUI components
- Implement view helpers if needed
- Set up Stimulus controllers
- Add Tailwind styles

### 5. Testing Implementation
```ruby
# spec/system/confirmation_flow_spec.rb
RSpec.describe "Confirmation Flow", type: :system do
  let(:invitation) { create(:invitation) }
  let(:participant) { create(:invitation_participant, invitation: invitation) }

  it "allows participant to confirm invitation" do
    visit confirmation_path(participant.token)
    # Test implementation
  end
end
```

## Development Workflow

### Step-by-Step Approach
1. Set up infrastructure (routes, models, basic controllers)
2. Implement core business logic
3. Create and style UI components
4. Add real-time updates with Hotwire
5. Write comprehensive tests
6. Document and review

### Test-Driven Process
- Write failing test first
- Implement minimum code to pass
- Refactor while keeping tests green
- Repeat for next feature confirmation feature in a Ruby on Rails application. The implementation follows modern Rails practices, utilizing Hotwire (Turbo + Stimulus) for real-time updates and RubyUI components for the user interface.

## Overview and Dependencies

### Required Files
- Implementation Plan: `.ai/confirmation-implememntation-plan.md`
- Models:
  - `app/models/invitation.rb`
  - `app/models/invitation_participant.rb`
  - `app/models/confirmation.rb`
- Routes: `config/routes.rb`
- Controllers: `app/controllers/confirmations_controller.rb`
- Views: `app/views/confirmations/`
- Components: `app/components/`
- Tests: `spec/`

### System Dependencies
- Ruby on Rails 8.1
- PostgreSQL
- Node.js (for Hotwire)
- Redis (for Action Cable)

### Implementation Plan
The plan is located in `.ai/confirmation-implememntation-plan.md` and contains detailed information about:
- Routing structure
- Required models and their relationships
- Controllers and their actions
- UI components and their properties
- Views and templates
- Testing requirements

### Framework and Development Standards

#### Rails Conventions
- Follow Ruby on Rails 8.1 conventions and best practices
- Use Rails zeitwerk autoloading
- Implement concerns for shared functionality
- Follow REST conventions for controllers
- Use strong parameters for data filtering

#### Frontend Architecture
- RubyUI components inherit from `RubyUI::BaseComponent`
- Hotwire/Turbo for real-time updates
- Stimulus controllers for client-side interactions
- Tailwind CSS for styling (configured in `config/tailwind.config.js`)

#### Database and Models
- Use Rails migrations for schema changes
- Follow Active Record naming conventions
- Implement model validations and callbacks
- Use PostgreSQL-specific features when beneficial

#### Testing Framework
- RSpec for all test types
- Factory Bot for test data
- System tests with Capybara
- Shoulda Matchers for model specs

## Implementation Approach

### 1. Rails Infrastructure Setup
```ruby
# config/routes.rb
resources :confirmations, only: [:show, :create], param: :token
```
- Set up routes with token-based URLs
- Configure locale files in `config/locales/`
- Set up any required initializers
- Configure ActiveJob backend

### 2. Model Layer Implementation
```ruby
# app/models/confirmation.rb
class Confirmation < ApplicationRecord
  belongs_to :invitation_participant
  validates :confirmed_at, presence: true
  # ... more validations and callbacks
end
```
- Implement model validations
- Set up model relationships
- Add required callbacks
- Create background jobs if needed

### 3. Controller and View Structure
```ruby
# app/controllers/confirmations_controller.rb
class ConfirmationsController < ApplicationController
  before_action :find_participant_by_token

  def show
    @confirmation = @participant.build_confirmation
  end

  def create
    # Implementation
  end
end
```
- Set up controller actions and filters
- Create view templates and partials
- Implement error handling
- Set up Turbo Stream responses

### 4. Business Logic (Backend):
- Implement controller actions
- Add error handling and validations
- Configure ActiveJob for retry logic
- Implement helper services

### 5. Interactivity (Frontend + Backend):
- Add Stimulus controllers where needed
- Configure Turbo Streams for real-time updates
- Implement loading states
- Add animations and transitions

### 6. Testing:
- Write RSpec tests for:
  - Models
  - Controllers
  - Components
  - Integration
- Implement system tests for full flow

## Step-by-Step Implementation

Implement in small, verified steps:

1. Complete first 3 tasks from current section
2. Test changes and ensure everything works
3. Summarize completed work
4. Describe plan for next 3 tasks
5. Stop and wait for feedback
6. After receiving approval, continue with next tasks

## Implementation Standards

### Backend:
- Use Repository pattern for complex queries
- Implement callbacks in models for business logic
- Use Service Objects for complex logic
- Utilize Active Job for asynchronous tasks
- Implement error handling through rescue_from

### Frontend:
- Components must inherit from RubyUI::BaseComponent
- Use Phlex for HTML generation
- Components should be stateless
- Use Tailwind for styling
- Implement full accessibility support

### Testing:
- One expectation per test
- Use subject for main test object
- Prefer eq over == for comparisons
- Test all edge cases
- Implement system tests for key paths

## Implementation Validation

After completing each section, ensure that:
1. Code follows Ruby on Rails conventions
2. All components are properly integrated
3. Tests pass and cover key functionality
4. UI is responsive and accessible
5. Performance is optimal
6. Error handling is complete
7. Documentation is up to date

## Implementation Priorities

1. Functional correctness
2. Compliance with Rails and RubyUI conventions
3. Test coverage
4. Accessibility
5. Performance
6. DRY and clean code
7. Documentation
