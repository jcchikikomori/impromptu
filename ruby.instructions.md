---
applyTo: "**/*.{rb,rake,ru,erb,haml,slim}"
---
# Ruby / Rails Instructions

## General
- Prioritize TDD (write tests first). If not feasible, still add tests immediately after.
- Prefer guard clauses for readability.
- Follow RuboCop rules and the repository's existing RuboCop config.
- Apply OWASP Top 10 when touching auth, sessions, input validation, or security-sensitive code.
- Prefer existing Rails patterns (models, concerns, service objects) already present in the codebase.

## Style Guides
- Ruby: https://github.com/rubocop-hq/ruby-style-guide
- Rails: https://github.com/rubocop-hq/rails-style-guide
- RSpec: http://www.betterspecs.org/

## Testing (RSpec)
- Use `let` for test data instead of instance variables.
- Use `is_expected` over `should`.
- Use `ActiveSupport::TimeHelpers` for time stubbing (in `around` blocks).
- Controller specs must include `render_views`.
- All specs require `rails_helper`.
- Expectations compared to **literal values**, not method calls:
  ```ruby
  # GOOD
  expect(foo.bar).to eq(1)

  # BAD
  expect(foo.bar).to eq(baz.spam)
  ```
- Test every controller action including:
  - Users not logged in
  - Users without permissions
- All model code and service classes must have unit tests.

## Security (Rails-specific)

### Input Handling
- Use **Strong Parameters** to whitelist attributes.
- Validate at application and database layers.
- File uploads: whitelist content types, set size limits.
- Rails escapes SQL by default - use parameterized queries.

### Authentication & Sessions
- Use **Devise** for authentication.
- Cookies: encrypted, signed, secure, http-only.
- Sessions: timeout after short period.
- Example session config:
  ```ruby
  Rails.application.config.session_store :cache_store, key: "_app_session",
    expire_after: 20.minutes, secure: true, httponly: true, same_site: :lax
  ```

### Authorization
- Use **cancancan** for RBAC (Role-Based Access Control).
- Default: deny access for any request requiring auth.
- Always use least necessary privilege.
- Validate abilities with every request.

### CSRF & XSS
- Never disable `protect_from_forgery`.
- Use Rails' default HTML escaping.

### Browser Security
- Use `X-Frame-Options` header (Rails default).
- Enable HSTS: `config.force_ssl = true` in production.
- Consider `secure_headers` gem.

### Sensitive Data
- Use `attr_encrypted` gem for field-level encryption (e.g., bank accounts).
- Passwords hashed with bcrypt + unique salts (Devise default).
- Strip sensitive fields before logging to external services.

## Database
- Avoid **N+1 queries**.
- Add **indexes** for columns referenced in queries.
- Use **soft delete** for deletions.
- Schema changes require team lead approval.
