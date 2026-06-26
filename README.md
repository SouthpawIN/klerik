# Klerik — The Code Review Agent

The quality guardian of the fleet. Klerik ensures code meets high standards through thorough review, best practices enforcement, and quality assurance.

## Installation

```bash
hermes profile install https://github.com/SouthpawIN/klerik
```

## Update

```bash
hermes profile update klerik
```

## What Does Klerik Do?

**Code review and quality assurance**

Klerik is your code's conscience. It reviews implementations, checks for best practices, identifies potential issues, and ensures your codebase maintains high quality standards. Think of Klerik as your personal senior engineer who reviews every piece of code before it goes to production.

## Example Prompts

**Code review:**
```
User: "Review my authentication middleware"

Klerik:
🔍 Code Review: authentication.js

✅ Strengths:
- Clean function structure
- Good error handling
- Proper async/await usage

⚠️  Issues Found:

1. [HIGH] Timing attack vulnerability
   Line 24: Password comparison using === operator
   Risk: Attackers can guess passwords byte-by-byte
   Fix: Use crypto.timingSafeEqual()

2. [MEDIUM] Insufficient error logging
   Line 31: Generic error message hides real issues
   Fix: Log specific error types while sanitizing sensitive data

3. [LOW] Missing JSDoc comments
   Lines 15-45: No documentation for public functions
   Fix: Add JSDoc with @param, @returns, @throws

4. [MEDIUM] No rate limiting check
   Before authentication: Should verify rate limit
   Fix: Add rate limiter middleware before auth

📊 Quality Score: 7.5/10
Recommendation: Fix HIGH issues before merging
```

**Best practices check:**
```
User: "Check if my React component follows best practices"

Klerik:
🔍 Best Practices Review: UserProfile.jsx

✅ Following best practices:
- Using React.memo for performance
- Proper prop types defined
- Accessibility attributes present

⚠️  Improvements needed:

1. [MEDIUM] Unnecessary re-renders
   Issue: Creating new objects in render
   ```
   // Before (re-creates on every render)
   const style = { color: user.isActive ? 'green' : 'red' }
   
   // After (stable reference)
   const style = useMemo(() => ({ 
     color: user.isActive ? 'green' : 'red' 
   }), [user.isActive])
   ```

2. [LOW] Missing error boundary
   Issue: No error handling for component tree
   Fix: Wrap in ErrorBoundary component

3. [MEDIUM] Accessibility: Missing alt text
   Line 34: Image without alt attribute
   Fix: Add descriptive alt text
```

**Security audit:**
```
User: "Audit my API endpoint for security issues"

Klerik:
🔒 Security Audit: POST /api/transactions

🚨 Critical Issues:

1. SQL Injection vulnerability (CRITICAL)
   Line 45: User input directly concatenated in SQL
   Risk: Complete database compromise
   Fix: Use parameterized queries
   ```
   // Before (VULNERABLE)
   const query = `SELECT * FROM users WHERE id = ${userId}`
   
   // After (SAFE)
   const query = 'SELECT * FROM users WHERE id = ?'
   db.query(query, [userId])
   ```

2. Mass Assignment (HIGH)
   Line 67: Accepting all user input directly
   Risk: Users can modify fields they shouldn't
   Fix: Whitelist allowed fields

⚠️  Medium Issues:

3. Insufficient authorization (MEDIUM)
   Missing: Ownership verification
   Risk: Users can access other users' data
   Fix: Verify userId matches authenticated user

4. No transaction validation (MEDIUM)
   Missing: Amount and balance checks
   Risk: Negative balances possible
   Fix: Add validation before processing

📊 Security Score: 3.2/10
Action Required: Fix all issues before production
```

**Performance review:**
```
User: "Is there performance I can improve?"

Klerik:
🚀 Performance Review: Dashboard.jsx

🔥 Hot Spots Found:

1. Unnecessary API calls
   Issue: Fetching data on every render
   Current: 47 API calls per second
   Fix: Cache with React Query
   Expected: 2 API calls per user action

2. Large bundle size
   Issue: Importing entire lodash library
   Current: 542KB added to bundle
   Fix: Import only needed functions
   ```
   // Before
   import _ from 'lodash'
   
   // After
   import debounce from 'lodash/debounce'
   ```
   Expected: 8KB added to bundle

3. Blocking main thread
   Issue: Heavy computation in useEffect (no deps)
   Fix: Move to Web Worker
   Expected: 60fps maintained during computation

📈 Potential Improvement: 3.2x faster load time
```

## Review Categories

### 🔒 Security
- Input validation
- Authentication & authorization
- Data sanitization
- Encryption usage
- Secret management

### 🚀 Performance
- Unnecessary re-renders
- Bundle size optimization
- Database query efficiency
- Caching opportunities
- Memory leaks

### 🧹 Code Quality
- Single Responsibility Principle
- DRY (Don't Repeat Yourself)
- Function length and complexity
- Naming conventions
- Error handling

### 📚 Documentation
- JSDoc/TSDoc comments
- README completeness
- API documentation
- Complex logic explanations
- Setup instructions

### ✅ Testing
- Test coverage
- Edge cases
- Integration tests
- Mock usage
- Test readability

### 🎯 Best Practices
- Framework-specific patterns
- Language idioms
- Design patterns
- Anti-patterns detection
- Modern syntax usage

## Advanced Features

### Automated Refactoring Suggestions
```
Klerik: "I found 5 opportunities to modernize your code:

1. Replace var with const/let (3 instances)
2. Use optional chaining (?.) for null checks (7 instances)
3. Convert callback-based functions to async/await (2 functions)
4. Use destructuring for object access (4 instances)
5. Replace for loops with array methods (6 loops)

Generate PR with these changes? [Y/n]"
```

### Historical Review
```
Klerik: "Comparing current code with 3 months ago:

📈 Improvements:
- Test coverage: 42% → 89% (+47%)
- Code complexity: High → Medium
- Security issues: 12 → 2 (-10)

⚠️  Regressions:
- Bundle size: 245KB → 512KB (+267KB)
- API response time: 120ms → 340ms (+220ms)

Recommendation: Investigate bundle bloat"
```

### Multi-language Projects
Klerik can review polyglot projects:
```
Frontend: TypeScript/React review
Backend: Python/Django review  
Database: SQL optimization
Infrastructure: Docker/Terraform review
```

## When to Use Klerik

- Before merging PRs
- After significant code changes
- Before deploying to production
- During pair programming sessions
- For onboarding code reviews
- Quarterly code quality audits
- Performance troubleshooting

## When to Use Other Agents

- **Chizul**: For implementing fixes Klerik identifies
- **Kashi**: For writing the documentation Klerik recommends
- **Senter**: For prioritizing which issues to fix first

## Integration with Git

Klerik can be configured as a git pre-push hook:
```bash
#!/bin/bash
# .git/hooks/pre-push

echo "Klerik reviewing changes..."
klerik review --diff $(git diff origin/main)

if [ $? -ne 0 ]; then
  echo "Klerik found issues. Please fix before pushing."
  exit 1
fi

echo "Klerik approved! ✓"
```

---

*Part of the multi-agent fleet by SouthpawIN*