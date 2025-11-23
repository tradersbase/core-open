# Contributing to TradersBase

Thank you for your interest in contributing to TradersBase! This document provides guidelines for contributing to the project.

---

## Ways to Contribute

### 🐛 Bug Reports
If you find a bug, please create an issue with:
- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Screenshots if applicable
- Browser/device information

### 💡 Feature Requests
We welcome feature suggestions! Please include:
- Clear description of the feature
- Use case and benefits
- Any implementation ideas
- Potential challenges

### 📝 Documentation
Help improve our documentation:
- Fix typos or unclear explanations
- Add examples and use cases
- Improve setup instructions
- Translate documentation

### 🎨 UI/UX Improvements
Suggestions for better user experience:
- Design improvements
- Accessibility enhancements
- Mobile optimization
- Performance improvements

---

## Getting Started

### Prerequisites
- Node.js 18+ installed
- Basic knowledge of React and TypeScript
- Familiarity with Solana blockchain (helpful)
- Understanding of REST APIs

### Setup
This is a public repository showcasing the project. For development access and contribution opportunities, please contact the team.

---

## Code Style

### TypeScript
- Use TypeScript for all new code
- Define proper types and interfaces
- Avoid `any` types when possible
- Use meaningful variable names

### React Components
- Functional components with hooks
- Props typed with interfaces
- Use destructuring for props
- Keep components focused and small

### CSS/Styling
- Use TailwindCSS utility classes
- Follow existing design patterns
- Maintain consistent spacing
- Ensure responsive design

### Naming Conventions
- Components: PascalCase (e.g., `TokenCard.tsx`)
- Functions: camelCase (e.g., `fetchTokenData`)
- Constants: UPPER_SNAKE_CASE (e.g., `API_BASE_URL`)
- Files: kebab-case or PascalCase

---

## Commit Guidelines

### Commit Messages
Follow conventional commit format:
```
type(scope): description

[optional body]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding tests
- `chore`: Maintenance tasks

Examples:
```
feat(risk): add new liquidity depth metric
fix(ui): resolve token card alignment issue
docs(readme): update installation instructions
```

---

## Pull Request Process

1. **Fork the repository** (when applicable)
2. **Create a feature branch**
   ```bash
   git checkout -b feat/your-feature-name
   ```
3. **Make your changes**
   - Write clean, documented code
   - Test your changes thoroughly
   - Update documentation if needed
4. **Commit your changes**
   - Follow commit message guidelines
   - Keep commits atomic and focused
5. **Push to your branch**
   ```bash
   git push origin feat/your-feature-name
   ```
6. **Open a Pull Request**
   - Clear description of changes
   - Reference any related issues
   - Include screenshots for UI changes

---

## Code Review

All contributions will be reviewed for:
- Code quality and style
- Functionality and correctness
- Performance implications
- Security considerations
- Documentation completeness

Please be patient during the review process and be open to feedback.

---

## Community Guidelines

### Be Respectful
- Treat all contributors with respect
- Welcome newcomers
- Provide constructive feedback
- Assume good intentions

### Communication
- Use clear and concise language
- Provide context for discussions
- Stay on topic
- Be professional

### Quality Standards
- Test your code before submitting
- Write clear documentation
- Follow project conventions
- Consider edge cases

---

## Questions?

If you have questions about contributing:
- Check existing issues and discussions
- Review documentation thoroughly
- Reach out to maintainers
- Join community discussions

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for helping make TradersBase better! 🚀**
