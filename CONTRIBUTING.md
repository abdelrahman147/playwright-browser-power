# Contributing to Playwright Browser Power

Thank you for your interest in contributing! This power is designed to give Kiro real eyes through browser automation, and we welcome improvements from the community.

## Ways to Contribute

### 1. Report Issues
- Found a bug? Open an issue!
- Have a feature request? We'd love to hear it!
- Documentation unclear? Let us know!

### 2. Improve Documentation
- Fix typos or unclear explanations
- Add more examples
- Improve troubleshooting guides
- Add framework-specific tips

### 3. Add Steering Files
- Create new workflow guides
- Add advanced patterns
- Share best practices
- Document edge cases

### 4. Share Examples
- Real-world use cases
- Integration patterns
- Testing strategies
- Performance tips

### 5. Test and Provide Feedback
- Try the power on different platforms
- Test with various frameworks
- Report compatibility issues
- Share success stories

## Getting Started

### Prerequisites
- Node.js 18+
- Kiro IDE installed
- Basic understanding of Playwright
- Familiarity with browser automation

### Setup for Development

1. **Fork and Clone**
```bash
git clone https://github.com/yourusername/playwright-browser-power.git
cd playwright-browser-power
```

2. **Install in Kiro**
```bash
# Copy to Kiro powers directory
cp -r playwright-browser ~/.kiro/powers/

# Or use local directory in Powers UI
```

3. **Test Your Changes**
- Open Kiro
- Try the power with various commands
- Verify documentation accuracy
- Test on your platform

## Contribution Guidelines

### Documentation Standards

**POWER.md:**
- Keep frontmatter fields accurate
- Use clear, concise language
- Include code examples
- Add troubleshooting tips

**Steering Files:**
- Focus on specific workflows
- Include step-by-step instructions
- Provide complete examples
- Explain the "why" not just the "how"

**README.md:**
- User-friendly language
- Quick start examples
- Clear installation steps
- Visual examples when possible

### Code Examples

**Good Example:**
```markdown
### Example: Test Login Flow

```
User: "test the login flow"
```

Kiro will:
1. Navigate to /login
2. Fill in credentials
3. Submit the form
4. Verify redirect to dashboard
5. Take screenshots at each step
```

**Bad Example:**
```markdown
### Login Testing
You can test login.
```

### Writing Style

✅ **Do:**
- Use active voice
- Be specific and concrete
- Include examples
- Explain edge cases
- Think about beginners

❌ **Don't:**
- Use jargon without explanation
- Assume prior knowledge
- Skip error handling
- Leave placeholders like "TODO"
- Use vague language

## Types of Contributions

### 🐛 Bug Reports

**Include:**
- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Your environment (OS, Node version, Kiro version)
- Error messages or logs
- Screenshots if relevant

**Template:**
```markdown
**Description:**
Brief description of the bug

**Steps to Reproduce:**
1. Step one
2. Step two
3. Step three

**Expected Behavior:**
What should happen

**Actual Behavior:**
What actually happens

**Environment:**
- OS: macOS 14.0
- Node: v20.0.0
- Kiro: v1.0.0
- Browser: Chromium 120.0

**Error Messages:**
```
Paste error messages here
```

**Screenshots:**
[Attach if relevant]
```

### ✨ Feature Requests

**Include:**
- Clear description of the feature
- Use case / problem it solves
- Proposed solution
- Alternative solutions considered
- Examples of similar features

**Template:**
```markdown
**Feature Description:**
Brief description

**Problem:**
What problem does this solve?

**Proposed Solution:**
How should it work?

**Use Case:**
Real-world example

**Alternatives:**
Other ways to solve this
```

### 📝 Documentation Improvements

**Include:**
- What's unclear or missing
- Proposed changes
- Why it's important
- Who benefits

### 🎯 New Steering Files

**Should Include:**
- Clear workflow description
- Step-by-step instructions
- Complete code examples
- Common errors and solutions
- When to use this workflow

**Template:**
```markdown
# Workflow Name

## Overview
Brief description of what this workflow does

## When to Use
- Use case 1
- Use case 2

## Prerequisites
- Requirement 1
- Requirement 2

## Step-by-Step Guide

### Step 1: [Action]
Description and code example

### Step 2: [Action]
Description and code example

## Common Issues
- Issue 1: Solution
- Issue 2: Solution

## Examples
Complete working examples

## Best Practices
- Tip 1
- Tip 2
```

## Pull Request Process

### Before Submitting

1. **Test your changes**
   - Verify on your platform
   - Test with multiple frameworks
   - Check for typos

2. **Update documentation**
   - Update CHANGELOG.md
   - Update relevant docs
   - Add examples if needed

3. **Follow conventions**
   - Match existing style
   - Use clear commit messages
   - Keep changes focused

### Submitting

1. **Create a branch**
```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

2. **Make your changes**
```bash
git add .
git commit -m "Add: clear description of changes"
```

3. **Push and create PR**
```bash
git push origin feature/your-feature-name
```

4. **Fill out PR template**
   - Describe your changes
   - Link related issues
   - Add screenshots if relevant
   - List testing done

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Other (describe)

## Related Issues
Fixes #123

## Changes Made
- Change 1
- Change 2
- Change 3

## Testing Done
- [ ] Tested on macOS
- [ ] Tested on Windows
- [ ] Tested on Linux
- [ ] Tested with React
- [ ] Tested with Vue
- [ ] Tested with other frameworks

## Screenshots
[If applicable]

## Checklist
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
- [ ] Examples tested
- [ ] No breaking changes
- [ ] Follows style guidelines
```

## Style Guidelines

### Markdown

- Use ATX-style headers (`#` not `===`)
- Use fenced code blocks with language tags
- Use tables for structured data
- Use lists for sequences
- Use bold for emphasis, not italics

### Code Examples

```markdown
# Good
```bash
npm run dev
```

# Bad
```
npm run dev
```
```

### Commit Messages

**Format:**
```
Type: Brief description

Longer explanation if needed
```

**Types:**
- `Add:` New feature or content
- `Fix:` Bug fix
- `Update:` Improve existing content
- `Remove:` Delete content
- `Docs:` Documentation only
- `Refactor:` Restructure without changing behavior

**Examples:**
```
Add: Quick start examples for React and Vue

Fix: Incorrect installation command for Linux

Update: Improve troubleshooting section with more details

Docs: Clarify browser installation process
```

## Community Guidelines

### Be Respectful
- Treat everyone with respect
- Be constructive in feedback
- Assume good intentions
- Help newcomers

### Be Clear
- Explain your reasoning
- Provide examples
- Ask questions if unclear
- Document your changes

### Be Patient
- Reviews take time
- Discussions are valuable
- Iteration improves quality
- Learning is part of the process

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Credited in relevant documentation
- Appreciated by the community! 🎉

## Questions?

- Open an issue for questions
- Tag with `question` label
- Check existing issues first
- Be specific about what you need

## License

By contributing, you agree that your contributions will be licensed under the same license as this project.

---

**Thank you for contributing!** Every improvement, no matter how small, makes this power better for everyone. 🚀
