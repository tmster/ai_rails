# AI Rules for RubyUI Development

## Overview

RubyUI is a UI component library for Ruby developers built on three core technologies:
- **Phlex**: A framework for building fast, reusable, testable views in pure Ruby
- **TailwindCSS**: A utility-first CSS framework for rapid custom designs
- **Stimulus JS**: A modest JavaScript framework for HTML enhancement

## Core Principles

### 1. Component-First Architecture
- All UI elements should be built as reusable Phlex components
- Components are Ruby classes that inherit from `Phlex::HTML`
- Each component has a `template` method (Phlex 1.x) or `view_template` method (Phlex 2.x)
- Components should be focused, single-purpose, and composable

### 2. Convention Over Configuration
- Follow Rails conventions for file organization and naming
- Use descriptive, meaningful names for components and methods
- Maintain consistent code style and structure across components

## Installation & Setup Rules

### Initial Setup
```bash
# Add RubyUI to development group only
bundle add ruby_ui --group development --require false

# Run the installer
bin/rails g ruby_ui:install

# Generate specific components as needed
bin/rails g ruby_ui:component Button
```

### Requirements
- Ruby 3.2 or later
- Rails application with TailwindCSS configured
- ESBuild or Importmaps for JavaScript bundling

## Component Structure Rules

### 1. Basic Component Anatomy
```ruby
class MyComponent < Phlex::HTML
  def initialize(title:, **attrs)
    @title = title
    @attrs = attrs
  end

  def template
    div(**@attrs) do
      h1(class: "text-xl font-bold") { @title }
      yield if block_given?
    end
  end
end
```

### 2. Component Naming Conventions
- Use PascalCase for component class names
- File names should be snake_case with `_component.rb` suffix
- Store components in `app/components/ruby_ui/` directory
- Use descriptive names that reflect component purpose

### 3. Parameter Handling
- Use keyword arguments for component initialization
- Provide sensible defaults where appropriate
- Accept `**attrs` for HTML attribute passthrough
- Validate required parameters in initializer

## Styling Rules

### 1. TailwindCSS Integration
- Use TailwindCSS utility classes exclusively for styling
- Avoid custom CSS unless absolutely necessary
- Leverage Tailwind's responsive and state modifiers
- Use Tailwind's design tokens for consistency

### 2. Class Management
```ruby
# Adding classes (appends to existing)
Button(class: 'w-full')

# Overriding classes (with !important)
Button(class: '!bg-red-500')

# Replacing all classes
Button(class!: 'bg-red-500 text-white py-2 px-4')
```

### 3. Theming Support
- Design components to support theming through CSS custom properties
- Use semantic color names rather than specific color values
- Make components responsive by default

## JavaScript Integration Rules

### 1. Stimulus Controller Integration
```ruby
# In component
div(
  data: {
    controller: "dropdown",
    action: "click->dropdown#toggle"
  }
) do
  # component content
end
```

### 2. Stimulus Best Practices
- Keep controllers focused and single-purpose
- Use private methods (prefixed with `#`) for internal logic
- Minimize public API surface
- Use targets and values for component communication
- Follow the connect/disconnect lifecycle

### 3. Progressive Enhancement
- Ensure components work without JavaScript
- Add JavaScript as enhancement, not requirement
- Use unobtrusive JavaScript patterns
- Handle edge cases and error states

## Component Creation Rules

### 1. Planning New Components
- Identify the component's single responsibility
- Define the required and optional parameters
- Consider reusability and composability
- Plan for accessibility from the start

### 2. Implementation Steps
1. Create the component class with proper inheritance
2. Define the initializer with keyword arguments
3. Implement the template/view_template method
4. Add appropriate TailwindCSS classes
5. Include Stimulus controllers if needed
6. Test component in isolation
7. Document usage patterns

### 3. Component Composition
```ruby
def template
  Card do
    CardHeader do
      CardTitle { @title }
    end

    CardContent do
      yield if block_given?
    end

    CardFooter do
      Button { "Action" }
    end
  end
end
```

## Usage in Views Rules

### 1. Rails Integration
```ruby
# In controllers
def show
  render MyComponent.new(title: "Hello World")
end

# In other components
def template
  render MyComponent.new(title: @title)
end
```

### 2. Block Handling
```ruby
# Component that accepts blocks
render Card.new do
  h2 { "Card Title" }
  p { "Card content goes here" }
end
```

### 3. Data Passing
- Pass only necessary data to components
- Use primitive types when possible
- Avoid passing complex objects unless needed
- Consider using presenters for complex data transformation

## Customization Rules

### 1. Component Extension
```ruby
class CustomButton < RubyUI::Button
  private

  def default_classes
    "bg-purple-500 hover:bg-purple-600 #{super}"
  end
end
```

### 2. Attribute Override
- Use class attributes for styling customization
- Implement data attributes for JavaScript behavior
- Support HTML attributes passthrough
- Provide escape hatches for edge cases

## Testing Rules

### 1. Component Testing
```ruby
RSpec.describe MyComponent do
  it "renders with correct markup" do
    component = MyComponent.new(title: "Test")
    html = component.call

    expect(html).to include("Test")
    expect(html).to match(/class="[^"]*text-xl[^"]*"/)
  end
end
```

### 2. Testing Guidelines
- Test component output, not implementation
- Test different parameter combinations
- Test block handling if applicable
- Test accessibility attributes
- Use Capybara for integration testing

## Performance Rules

### 1. Optimization
- Leverage Phlex's performance benefits (12x faster than ERB)
- Minimize object allocation in component methods
- Use memoization for expensive calculations
- Avoid unnecessary DOM updates

### 2. Bundle Management
- Only install components you actually use
- Use tree-shaking with JavaScript bundlers
- Minimize CSS bundle size through purging
- Load Stimulus controllers lazily when possible

## Accessibility Rules

### 1. Semantic HTML
- Use appropriate HTML elements for content structure
- Include ARIA attributes where necessary
- Ensure proper heading hierarchy
- Provide alternative text for images

### 2. Keyboard Navigation
- Ensure all interactive elements are keyboard accessible
- Implement proper focus management
- Use logical tab order
- Provide focus indicators

### 3. Screen Reader Support
- Use semantic markup
- Provide appropriate labels and descriptions
- Handle dynamic content updates
- Test with actual screen readers

### 2. Usage Examples
- Provide clear, working examples
- Show different configuration options
- Include integration patterns
- Document edge cases and limitations

## Error Handling Rules

### 1. Graceful Degradation
- Handle missing parameters gracefully
- Provide meaningful error messages
- Fail early for critical errors
- Use sensible fallbacks where appropriate

### 2. Validation
```ruby
def initialize(variant:, **attrs)
  validate_variant(variant)
  @variant = variant
  @attrs = attrs
end

private

def validate_variant(variant)
  valid_variants = [:primary, :secondary, :outline]
  unless valid_variants.include?(variant)
    raise ArgumentError, "Invalid variant: #{variant}. Must be one of #{valid_variants}"
  end
end
```

## Security Rules

### 1. XSS Prevention
- Phlex automatically escapes content by default
- Use `unsafe_raw` only when absolutely necessary
- Validate and sanitize user input
- Be careful with dynamic attribute generation

### 2. Data Handling
- Don't expose sensitive data in component attributes
- Validate data types and ranges
- Use strong parameters in Rails controllers
- Sanitize HTML content when needed

## Common Patterns

### 1. Conditional Rendering
```ruby
def template
  div(class: classes) do
    h1 { @title } if @title
    yield if block_given?
    render_footer if show_footer?
  end
end
```

### 2. Dynamic Classes
```ruby
private

def classes
  base_classes = "flex items-center"
  variant_classes = variant_class_map[@variant]
  size_classes = size_class_map[@size]

  [base_classes, variant_classes, size_classes].compact.join(" ")
end
```

### 3. Slot Pattern
```ruby
def template
  article(class: "card") do
    header(class: "card-header") { @header_content } if @header_content
    main(class: "card-body") { yield }
    footer(class: "card-footer") { @footer_content } if @footer_content
  end
end
```

# Documentation

Further reading available under https://rubyui.com/docs/introduction

# RubyUI Components - Complete Class Reference for predefined components.
Try to avoid defining your own components

## Accordion
```ruby
RubyUI::Accordion::Accordion
RubyUI::Accordion::AccordionContent
RubyUI::Accordion::AccordionDefaultContent
RubyUI::Accordion::AccordionDefaultTrigger
RubyUI::Accordion::AccordionIcon
RubyUI::Accordion::AccordionItem
RubyUI::Accordion::AccordionTrigger
```

## Alert
```ruby
RubyUI::Alert::Alert
RubyUI::Alert::AlertDescription
RubyUI::Alert::AlertTitle
```

## AlertDialog
```ruby
RubyUI::AlertDialog::AlertDialog
RubyUI::AlertDialog::AlertDialogAction
RubyUI::AlertDialog::AlertDialogCancel
RubyUI::AlertDialog::AlertDialogContent
RubyUI::AlertDialog::AlertDialogDescription
RubyUI::AlertDialog::AlertDialogFooter
RubyUI::AlertDialog::AlertDialogHeader
RubyUI::AlertDialog::AlertDialogTitle
RubyUI::AlertDialog::AlertDialogTrigger
```

## AspectRatio
```ruby
RubyUI::AspectRatio::AspectRatio
```

## Avatar
```ruby
RubyUI::Avatar::Avatar
RubyUI::Avatar::AvatarFallback
RubyUI::Avatar::AvatarImage
```

## Badge
```ruby
RubyUI::Badge::Badge
```

## Breadcrumb
```ruby
RubyUI::Breadcrumb::Breadcrumb
RubyUI::Breadcrumb::BreadcrumbEllipsis
RubyUI::Breadcrumb::BreadcrumbItem
RubyUI::Breadcrumb::BreadcrumbLink
RubyUI::Breadcrumb::BreadcrumbList
RubyUI::Breadcrumb::BreadcrumbPage
RubyUI::Breadcrumb::BreadcrumbSeparator
```

## Button
```ruby
RubyUI::Button::Button
```

## Calendar
```ruby
RubyUI::Calendar::Calendar
RubyUI::Calendar::CalendarBody
RubyUI::Calendar::CalendarDays
RubyUI::Calendar::CalendarHeader
RubyUI::Calendar::CalendarNext
RubyUI::Calendar::CalendarPrev
RubyUI::Calendar::CalendarTitle
RubyUI::Calendar::CalendarWeekdays
```

## Card
```ruby
RubyUI::Card::Card
RubyUI::Card::CardContent
RubyUI::Card::CardDescription
RubyUI::Card::CardFooter
RubyUI::Card::CardHeader
RubyUI::Card::CardTitle
```

## Carousel
```ruby
RubyUI::Carousel::Carousel
RubyUI::Carousel::CarouselContent
RubyUI::Carousel::CarouselItem
RubyUI::Carousel::CarouselNext
RubyUI::Carousel::CarouselPrevious
```

## Chart
```ruby
RubyUI::Chart::Chart
```

## Checkbox
```ruby
RubyUI::Checkbox::Checkbox
RubyUI::Checkbox::CheckboxGroup
```

## Clipboard
```ruby
RubyUI::Clipboard::Clipboard
RubyUI::Clipboard::ClipboardPopover
RubyUI::Clipboard::ClipboardSource
RubyUI::Clipboard::ClipboardTrigger
```

## Codeblock
```ruby
RubyUI::Codeblock::Codeblock
```

## Collapsible
```ruby
RubyUI::Collapsible::Collapsible
RubyUI::Collapsible::CollapsibleContent
RubyUI::Collapsible::CollapsibleTrigger
```

## Combobox
```ruby
RubyUI::Combobox::Combobox
RubyUI::Combobox::ComboboxCheckbox
RubyUI::Combobox::ComboboxEmptyState
RubyUI::Combobox::ComboboxItem
RubyUI::Combobox::ComboboxList
RubyUI::Combobox::ComboboxListGroup
RubyUI::Combobox::ComboboxPopover
RubyUI::Combobox::ComboboxRadio
RubyUI::Combobox::ComboboxSearchInput
RubyUI::Combobox::ComboboxToggleAllCheckbox
RubyUI::Combobox::ComboboxTrigger
```

## Command
```ruby
RubyUI::Command::Command
RubyUI::Command::CommandDialog
RubyUI::Command::CommandDialogContent
RubyUI::Command::CommandDialogTrigger
RubyUI::Command::CommandEmpty
RubyUI::Command::CommandGroup
RubyUI::Command::CommandInput
RubyUI::Command::CommandItem
RubyUI::Command::CommandList
```

## ContextMenu
```ruby
RubyUI::ContextMenu::ContextMenu
RubyUI::ContextMenu::ContextMenuContent
RubyUI::ContextMenu::ContextMenuItem
RubyUI::ContextMenu::ContextMenuLabel
RubyUI::ContextMenu::ContextMenuSeparator
RubyUI::ContextMenu::ContextMenuTrigger
```

## Dialog
```ruby
RubyUI::Dialog::Dialog
RubyUI::Dialog::DialogContent
RubyUI::Dialog::DialogDescription
RubyUI::Dialog::DialogFooter
RubyUI::Dialog::DialogHeader
RubyUI::Dialog::DialogMiddle
RubyUI::Dialog::DialogTitle
RubyUI::Dialog::DialogTrigger
```

## DropdownMenu
```ruby
RubyUI::DropdownMenu::DropdownMenu
RubyUI::DropdownMenu::DropdownMenuContent
RubyUI::DropdownMenu::DropdownMenuItem
RubyUI::DropdownMenu::DropdownMenuLabel
RubyUI::DropdownMenu::DropdownMenuSeparator
RubyUI::DropdownMenu::DropdownMenuTrigger
```

## Form
```ruby
RubyUI::Form::Form
RubyUI::Form::FormField
RubyUI::Form::FormFieldError
RubyUI::Form::FormFieldHint
RubyUI::Form::FormFieldLabel
```

## HoverCard
```ruby
RubyUI::HoverCard::HoverCard
RubyUI::HoverCard::HoverCardContent
RubyUI::HoverCard::HoverCardTrigger
```

## Input
```ruby
RubyUI::Input::Input
```

## Link
```ruby
RubyUI::Link::Link
```

## MaskedInput
```ruby
RubyUI::MaskedInput::MaskedInput
```

## Pagination
```ruby
RubyUI::Pagination::Pagination
RubyUI::Pagination::PaginationContent
RubyUI::Pagination::PaginationEllipsis
RubyUI::Pagination::PaginationItem
```

## Popover
```ruby
RubyUI::Popover::Popover
RubyUI::Popover::PopoverContent
RubyUI::Popover::PopoverTrigger
```

## Progress
```ruby
RubyUI::Progress::Progress
```

## RadioButton
```ruby
RubyUI::RadioButton::RadioButton
```

## Select
```ruby
RubyUI::Select::Select
RubyUI::Select::SelectContent
RubyUI::Select::SelectGroup
RubyUI::Select::SelectInput
RubyUI::Select::SelectItem
RubyUI::Select::SelectLabel
RubyUI::Select::SelectTrigger
RubyUI::Select::SelectValue
```

## Separator
```ruby
RubyUI::Separator::Separator
```

## Sheet
```ruby
RubyUI::Sheet::Sheet
RubyUI::Sheet::SheetContent
RubyUI::Sheet::SheetDescription
RubyUI::Sheet::SheetFooter
RubyUI::Sheet::SheetHeader
RubyUI::Sheet::SheetMiddle
RubyUI::Sheet::SheetTitle
RubyUI::Sheet::SheetTrigger
```

## ShortcutKey
```ruby
RubyUI::ShortcutKey::ShortcutKey
```

## Sidebar
```ruby
RubyUI::Sidebar::CollapsibleSidebar
RubyUI::Sidebar::MobileSidebar
RubyUI::Sidebar::NonCollapsibleSidebar
RubyUI::Sidebar::Sidebar
RubyUI::Sidebar::SidebarContent
RubyUI::Sidebar::SidebarFooter
RubyUI::Sidebar::SidebarGroup
RubyUI::Sidebar::SidebarGroupAction
RubyUI::Sidebar::SidebarGroupContent
RubyUI::Sidebar::SidebarGroupLabel
RubyUI::Sidebar::SidebarHeader
RubyUI::Sidebar::SidebarInput
RubyUI::Sidebar::SidebarInset
RubyUI::Sidebar::SidebarMenu
RubyUI::Sidebar::SidebarMenuAction
RubyUI::Sidebar::SidebarMenuBadge
RubyUI::Sidebar::SidebarMenuItem
RubyUI::Sidebar::SidebarMenuSkeleton
RubyUI::Sidebar::SidebarMenuSub
RubyUI::Sidebar::SidebarMenuSubButton
RubyUI::Sidebar::SidebarMenuSubItem
RubyUI::Sidebar::SidebarRail
RubyUI::Sidebar::SidebarSeparator
RubyUI::Sidebar::SidebarTrigger
RubyUI::Sidebar::SidebarWrapper
```

## Skeleton
```ruby
RubyUI::Skeleton::Skeleton
```

## Switch
```ruby
RubyUI::Switch::Switch
```

## Table
```ruby
RubyUI::Table::Table
RubyUI::Table::TableBody
RubyUI::Table::TableCaption
RubyUI::Table::TableCell
RubyUI::Table::TableFooter
RubyUI::Table::TableHead
RubyUI::Table::TableHeader
RubyUI::Table::TableRow
```

## Tabs
```ruby
RubyUI::Tabs::Tabs
RubyUI::Tabs::TabsContent
RubyUI::Tabs::TabsList
RubyUI::Tabs::TabsTrigger
```

## Textarea
```ruby
RubyUI::Textarea::Textarea
```

## ThemeToggle
```ruby
RubyUI::ThemeToggle::SetDarkMode
RubyUI::ThemeToggle::SetLightMode
RubyUI::ThemeToggle::ThemeToggle
```

## Tooltip
```ruby
RubyUI::Tooltip::Tooltip
RubyUI::Tooltip::TooltipContent
RubyUI::Tooltip::TooltipTrigger
```

## Typography
```ruby
RubyUI::Typography::Heading
RubyUI::Typography::InlineCode
RubyUI::Typography::InlineLink
RubyUI::Typography::Text
RubyUI::Typography::TypographyBlockquote
```
---

*These rules should be followed when developing or assisting with RubyUI projects to ensure consistency, maintainability, and best practices.*