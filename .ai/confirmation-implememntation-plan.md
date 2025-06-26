```markdown
# Invitation Detail (Participant) Implementation Plan

## 1. Overview
- **View Purpose:**
  Provide a public view for participants to review invitation details, select a time slot, and confirm attendance.
- **Key Features:**
  - Display meeting details (title, description, duration).
  - Showcase candidate time slots using a TimeSlotSelector.
  - Allow participants to confirm their attendance with a ConfirmationButton.
  - Validate secure token from the URL.
  - Mobile-optimized layout with clear CTAs.
- **Technical Approach:**
  - Use Rails controllers and views with Hotwire Turbo Streams for real-time updates.
  - Leverage RubyUI components (if applicable) for UI consistency.
  - Follow Rails 8.1 conventions and repository pattern (if complex query requirements arise).

## 2. Routes
- **Route Definitions:**
  - A custom GET route matching `/i/:secure_token` for public access.

```ruby
# config/routes.rb
Rails.application.routes.draw do
  # Invitation detail route for participants using secure token
  get '/i/:secure_token', to: 'invitations#show', as: :invitation_detail
  # ...existing routes...
end
```

## 3. Models
- **Schema and Relationships:**
  - **Invitation:** Contains meeting title, duration, description and unique secure_token.
  - **InvitationParticipant:** Associates invitations with participants and holds email, secure_token, etc.
  - **TimeSlot:** Contains potential meeting times and is linked to InvitationParticipant.
  - **Confirmation:** Records participant confirmation timestamps.
- **Requirements/Constraints:**
  - Secure token uniqueness and presence.
  - Validations as defined in the current models.
- **Potential Challenges:**
  - Ensuring efficient query performance when joining related models.
  - Handling cases where the secure token is invalid.

## 4. Controllers
- **Controller:** `InvitationsController`
- **Required Action:**
  - `show`: Locates the invitation using the secure token, fetches associated time slots, and renders the view.
- **Before/After Filters:**
  - Filter to verify the secure token and handle errors (e.g., token not found).
- **Strong Parameters:** Not needed for this GET action.
- **Error Handling:**
  - Render a 404 page for invalid tokens.
  - Log error details for debugging purposes.

```ruby
# app/controllers/invitations_controller.rb
class InvitationsController < ApplicationController
  before_action :find_invitation_by_token, only: [:show]

  def show
    # Fetch associated participant record if needed
    @participant = @invitation.invitation_participants.find_by(secure_token: params[:secure_token])
    # Prepare TimeSlots and other necessary data for the view
    @time_slots = @participant.time_slots if @participant
    # Render view with Turbo Frames if needed
  end

  private

  def find_invitation_by_token
    @invitation = Invitation.find_by(secure_token: params[:secure_token])
    unless @invitation
      render file: Rails.root.join('public', '404.html'), status: :not_found and return
    end
  end
end
```

## 5. Views
- **Template Hierarchy & Partials:**
  - Main template: `app/views/invitations/show.html.erb`
  - Partials:
    - `_public_view.html.erb` – displays meeting details and organizer info.
    - `_time_slot_selector.html.erb` – displays candidate time slots.
    - `_confirmation_button.html.erb` – includes a button/CTA to confirm attendance.
- **Helper Methods:**
  - Methods to format date/time.
  - Conditional helpers for displaying error messages.
- **Turbo Frames/Streams:**
  - Wrap time slot selection and confirmation actions within Turbo Frames for real-time updates.

```erb
<!-- app/views/invitations/show.html.erb -->
<%= render 'public_view', invitation: @invitation %>

<%= turbo_frame_tag "time_slots" do %>
  <%= render 'time_slot_selector', time_slots: @time_slots %>
<% end %>

<%= turbo_frame_tag "confirmation" do %>
  <%= render 'confirmation_button', invitation: @invitation, participant: @participant %>
<% end %>
```

## 6. Components (Optional / RubyUI Integration)
- **Component Hierarchy:**
  - **PublicView Component:** Renders invitation details with organizer info.
  - **TimeSlotSelector Component:** Renders a list of available slots.
  - **ConfirmationButton Component:** Renders a button to confirm attendance.
- **Props/Parameters:**
  - Accept necessary data such as title, description, time slots.
- **Templates:**
  - Each component should have its own template following RubyUI conventions.
- **Preview Examples:**
  - Include previews in `app/components/previews/` if using ViewComponent or RubyUI.

## 7. JavaScript
- **Stimulus Controllers:**
  - Controller to handle slot selection and confirmation actions.
  - Example: A `confirmation` controller to handle click events and provide Turbo updates.
- **Custom Modules:**
  - Basic validations or animations for mobile optimization.
- **Third-Party Integrations:**
  - None required for MVP as per PRD.

## 8. Testing Plan
- **Model Specs:**
  - Verify model validations and associations.
- **Controller Specs:**
  - Test the `show` action with both valid and invalid tokens.
- **View Specs:**
  - Ensure the main page renders all required components.
- **System Tests:**
  - Integration tests simulating a participant accessing the invitation.
- **API Tests:**
  - Not applicable here unless confirming attendance is handled via an API endpoint.

## 9. Implementation Steps
1. **Define Route:**
   - Add the route in `config/routes.rb` for `/i/:secure_token`.
2. **Update Controller:**
   - Implement the `show` action in `InvitationsController`.
   - Add token validation logic.
3. **Create View Template & Partials:**
   - Create `show.html.erb` and required partials under `app/views/invitations/`.
4. **Add Helper Methods:**
   - Implement methods for formatting date/time and handling conditional display.
5. **Turbo Integration:**
   - Wrap time slot and confirmation elements in Turbo Frames.
6. **JavaScript Enhancement:**
   - Create Stimulus controller(s) if additional client-side interactions are needed.
7. **Testing:**
   - Write RSpec tests for models, controller actions, and integration/system tests.
8. **Peer Review & Documentation:**
   - Ensure commit messages follow Conventional Commits and include the Jira ticket ID.
   - Update documentation if necessary.

## 10. Error Handling
- **Validation Errors:**
  - Handle cases where no invitation or participant is found.
  - Display inline error messages in the view.
- **Edge Cases:**
  - Token expired or re-used tokens.
  - Multiple participants with the same token.
- **Error Pages:**
  - Render a custom 404 page for invalid tokens.
- **Logging Strategy:**
  - Log token mismatch or lookup errors using Rails logger for audit and debugging.

```

This plan outlines a comprehensive approach to implementing the Invitation Detail view for participants. Follow the steps and guidelines to ensure coding best practices and robust error handling.
