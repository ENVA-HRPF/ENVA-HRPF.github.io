---
title: "DevTeam Wiki"
---

# DevTeam Wiki

This is a single-page wiki for our development team.

## Table of Contents
{{< toc >}}

## Code Style Guidelines

### General Principles

* Write readable, self-documenting code
* Prioritize clarity over cleverness
* Follow the DRY (Don't Repeat Yourself) principle
* Write testable code
* Add comments only when necessary to explain "why", not "what"

### Naming Conventions

* Use descriptive, meaningful names
* Follow camelCase for JavaScript/TypeScript variables
* Use snake_case for Python variables

| Good                  | Bad     |
|-----------------------|---------|
| `userData`            | `ud`    |
| `isValidResponse`     | `valid` |
| `calculateTotalPrice` | `calc`  |

### JavaScript Style

#### File Organization

* One class per file
* Group related functionality
* Import statements at the top
* Export statements at the bottom

#### Code Formatting

* Use 2 spaces for indentation
* Maximum line length: 100 characters
* Always use semicolons
* Use single quotes for strings

```javascript
// Example of well-formatted JavaScript code
class UserService {
  constructor(apiClient) {
    this.apiClient = apiClient;
    this.cache = new Map();
  }

  async getUserById(userId) {
    // Check cache first
    if (this.cache.has(userId)) {
      return this.cache.get(userId);
    }
    
    // Fetch from API if not in cache
    try {
      const user = await this.apiClient.get(`/users/${userId}`);
      this.cache.set(userId, user);
      return user;
    } catch (error) {
      console.error('Failed to fetch user:', error);
      throw new Error(`Unable to retrieve user with ID ${userId}`);
    }
  }
}
```

### Python Style

* Follow PEP 8
* Use type hints for function parameters and return values
* Use docstrings for all public functions and classes

```python
from typing import Dict, Optional, List
import logging

logger = logging.getLogger(__name__)

class DataProcessor:
    """Processes input data and generates reports."""
    
    def __init__(self, config: Dict[str, any]):
        """Initialize with configuration dictionary.
        
        Args:
            config: Configuration parameters
        """
        self.config = config
        self.initialized = False
    
    def process_batch(self, items: List[Dict]) -> Optional[Dict]:
        """Process a batch of items.
        
        Args:
            items: List of item dictionaries to process
            
        Returns:
            Summary of processing results or None if processing failed
        """
        if not items:
            return None
            
        try:
            # Processing logic here
            results = {'processed': len(items), 'failed': 0}
            return results
        except Exception as e:
            logger.error(f"Processing failed: {str(e)}")
            return None
```

### Linting and Formatting

All code must pass linting before it can be merged:

* JavaScript/TypeScript: ESLint + Prettier
* Python: flake8 + black
* CSS/SCSS: stylelint

## Git Workflow

### Branch Structure

We use a simplified GitFlow workflow with the following branches:

* `master`: Production code. Tagged with releases.
* `develop`: Development branch containing next release features.
* `feature/*`: Feature branches created from `develop`.
* `hotfix/*`: Emergency fixes for production.

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Types:

* `feat`: A new feature
* `fix`: A bug fix
* `docs`: Documentation changes
* `style`: Formatting changes
* `refactor`: Code change that neither fixes a bug nor adds a feature
* `test`: Adding or correcting tests
* `chore`: Changes to the build process or auxiliary tools

Good Commit Message Example:
```
feat(auth): implement JWT authentication

- Add token generation service
- Create middleware for token validation
- Update user model with token fields

Resolves: #123
```

{{% notice tip %}}
Keep your commit messages clear and descriptive. They are part of the project documentation!
{{% /notice %}}

## Code Review Process

### Why We Review Code

* Knowledge sharing
* Consistent coding practices
* Early bug detection
* Collective code ownership
* Mentoring opportunities

### Review Checklist

- [ ] Code follows our style guidelines
- [ ] Tests are included and passing
- [ ] Documentation is updated
- [ ] The code solves the intended problem
- [ ] No unnecessary complexity or over-engineering
- [ ] No security vulnerabilities
- [ ] No performance issues

{{% notice note %}}
Code reviews should focus on the code, not the person. Be kind and respectful in your feedback.
{{% /notice %}}

### Review Etiquette

#### For Reviewers
* Be kind and respectful
* Explain "why" in addition to "what"
* Use questions rather than statements when applicable
* Provide examples when suggesting changes
* Acknowledge good patterns and clever solutions

#### For Code Authors
* Don't take feedback personally
* Explain your approach when necessary
* Be open to alternative solutions
* Say "thank you" for helpful feedback

{{% notice important %}}
Security issues must be addressed before a PR can be approved.
{{% /notice %}}