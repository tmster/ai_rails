# Ruby on Rails 8.1 Convention
- Always use Hotwire Turbo Streams for real-time updates instead of custom JS
- Follow repository pattern for complex database queries
- Use Rubocop with custom rules from `.rubocop.yml`

# RSpec Best Practices
- One expectation per example
- Use `subject` for main test object
- Prefer `eq` over `==` for equality checks

# PostgreSQL Optimization
- Use materialized views for complex reports
- Prefer `jsonb` over `json` for unstructured data
- Implement full-text search with `pg_search` gem

# Workflow Rules
- Commit messages follow Conventional Commits
- PR descriptions must include Jira ticket ID
- Never push directly to `main` branch
- app is located under ai_rails subdirectory
