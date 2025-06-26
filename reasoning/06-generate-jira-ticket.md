You are an experienced product manager tasked with creating a jira ticket based on the following descriptions:

<prd>
put here prd part
</prd>

Follow these steps to create a comprehensive and well-organized document. Follow the comments in the template, dont include them in the final document
<template>
# Ticket Title: <Enter a concise and descriptive title here>

---

## Why
<!--
Provide the business rationale and context for this change or feature.
- What problem does this solve?
- How does this feature add value to the business or user?
- Include any dependency or blocking ticket references, e.g., "Blocked by [CP-2461](https://consultport.atlassian.net/browse/CP-2461)"
-->

---

## Requirements
<!--
List and detail all the requirements that need to be met:
- Core functionality or user story (e.g., "Agency Project Managers can create and send invoices directly to VMS clients")
- Any role restrictions or permissions
- Data and process requirements
-->

- [ ] Requirement 1: <Describe requirement>
- [ ] Requirement 2: <Describe requirement>
- [ ] Additional acceptance criteria as needed

---

## Specifications
<!--
Detail the implementation specifics. This section should include:
- Design references (e.g., Figma links)
- UI element interactions (buttons, toggles, modal dialogues, etc.)
- Field and form details (editable fields, default values, validations, etc.)
- Workflow or user flow descriptions (e.g., which page opens, what actions are performed)
-->

- **Design References:** [Insert link]
- **Entry Point / User Flow:**
  - Describe the entry point (e.g., "When the Activity Tracker for the billing period is added and the Agency has Invoice data, enable the [Create & Submit] button.")
  - List out the step-by-step flow of actions

- **Form Details:**
  - Billed by: Input field pre-populated with agency details
  - Billed to: Input field pre-populated with client details
  - Additional information (e.g., TAX ID, address)

- **Invoice Actions:**
  - Toggle to mark invoices as paid (visible based on roles)
  - Modal confirmation on action

- **Table Views / Admin Panel:**
  - Columns to include (e.g., Invoice ID, Project, Agency, Consultant, Client, Billing period, Status, Created Date)
  - Navigation settings for different types of invoices (e.g., VMS vs. Consultport Marketplace)

---

## Detailed Change Instructions
<!--
Outline any specific changes or conditions:
- What text, labels, or tooltips should be displayed (include different language translations if applicable)
- Specify cases where there is a difference in behavior between user roles (Agency Project Manager vs. Consultant)
- Note any importance of real-time updates or automatic changes (e.g., on_change toggles)
-->

- Describe any updates to existing pages (e.g., "Invoice Show page adjustments: no edit button, no reject button, add additional agency information")
- Define the conditions under which the view changes when accessing invoices

---

## Attachments / Screenshots
<!--
Attach or embed screenshots, design mockups, flow diagrams, or any additional assets.
Use Markdown image linking for screenshots with captions.
-->

![Screenshot Example](https://path/to/screenshot.png)

---

## Dependency and Blocking
<!--
List any related tickets, dependencies, or blockers.
-->

- Blocked by: [Ticket CP-2461](https://consultport.atlassian.net/browse/CP-2461)
- Additional dependency: [Ticket CP-2284](https://consultport.atlassian.net/browse/CP-2284)

---

## Translation Guidelines (YML Translate Section)
<!--
For any YML parts in the ticket (e.g., translations for UI elements), provide translations in multiple languages as needed.
Add a translations section where YML elements are listed verbatim and translated for internationalization.
Example translations:
-->
```yml
translations:
  en:
    invoice_paid_toggle: "Paid?"
    invoice_toggle_info: "Toggle to mark the invoice as paid."
  de:
    invoice_paid_toggle: "Bezahlt?"
    invoice_toggle_info: "Umschalten, um die Rechnung als bezahlt zu markieren."
  fr:
    invoice_paid_toggle: "Payé?"
    invoice_toggle_info: "Basculez pour marquer la facture comme payée."
```
*Note: Be sure to update any YML configuration files with the corresponding translations as per the design specifications.*

---

## Additional Notes
<!--
Include any additional information, context, or clarifications required by the development team.
- Mention any quick workarounds or suggestions for future iterations.
- Ensure any business rules or edge cases are documented.
-->
</template>

Remember to fill in each section with detailed, relevant information based on the project description and our clarifying questions. Make sure that the ticket is comprehensive, clear, and contains all the relevant information needed to continue working on the product.

The final result should consist solely of a ticket compliant with the specified format in markdown, which you will output.
