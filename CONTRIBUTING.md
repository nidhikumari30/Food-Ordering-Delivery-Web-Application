# Contributing to Food-Ordering-Delivery-Web-Application

Thank you for your interest in contributing to this project! This document provides guidelines and instructions for contributing.

## 🤝 How to Contribute

### Reporting Bugs
Before creating a bug report, please check the issue list to avoid duplicates. When creating a bug report, include:

- **Title**: Clear, descriptive title
- **Description**: Detailed description of the bug
- **Steps to Reproduce**: Exact steps to reproduce the issue
- **Expected Behavior**: What should happen
- **Actual Behavior**: What actually happens
- **Screenshots/Logs**: If applicable
- **Environment**: OS, Node version, Java version, etc.

### Suggesting Enhancements
Enhancement suggestions are tracked as GitHub Issues. When suggesting an enhancement, include:

- **Title**: Clear, descriptive title
- **Description**: Detailed description of the enhancement
- **Use Case**: Why this enhancement would be useful
- **Possible Implementation**: If you have ideas on implementation

### Pull Requests
1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Make** your changes
4. **Test** your changes thoroughly
5. **Commit** with clear messages (`git commit -m 'Add: Description of changes'`)
6. **Push** to your branch (`git push origin feature/AmazingFeature`)
7. **Open** a Pull Request with a clear description

## 💻 Development Setup

### Prerequisites
- Node.js v14+
- Java 17
- Maven 3.6+
- MySQL 8.0+

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/nidhikumari30/Food-Ordering-Delivery-Web-Application.git
   cd Food-Ordering-Delivery-Web-Application
   ```

2. **Setup Backend**
   ```bash
   cd food-ordering-app/food-order-back
   mvn clean install
   mvn spring-boot:run
   ```

3. **Setup Frontend** (in another terminal)
   ```bash
   cd food-ordering-app/food-ordering-front
   npm install
   npm start
   ```

## 📝 Code Style Guidelines

### Java Code Style
- Follow Google Java Style Guide
- Use meaningful variable names
- Keep methods small and focused
- Add comments for complex logic
- Use proper exception handling

### JavaScript/React Code Style
- Use ES6+ features
- Follow Airbnb JavaScript Style Guide
- Use functional components with hooks
- Props validation with PropTypes
- Meaningful component and variable names

### General Guidelines
- Use consistent indentation (2 spaces for JS, 4 for Java)
- Keep lines under 100 characters
- Use descriptive commit messages
- Add comments for non-obvious code
- Write clean, readable code

## 🧪 Testing

### Backend Testing
```bash
cd food-ordering-app/food-order-back
mvn test
```

### Frontend Testing
```bash
cd food-ordering-app/food-ordering-front
npm test
```

Ensure all tests pass before submitting a PR.

## 📋 Commit Message Format

Use clear, descriptive commit messages:

```
<type>: <subject>

<body>

<footer>
```

### Types
- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Code change that improves performance
- **test**: Adding or updating tests

### Examples
```
feat: Add user profile management
fix: Resolve JWT token expiration issue
docs: Update installation instructions
refactor: Improve database query efficiency
```

## 🔍 Code Review Process

Pull requests will be reviewed by maintainers. Review criteria:

- ✅ Code follows style guidelines
- ✅ All tests pass
- ✅ New tests added for new features
- ✅ Documentation is updated
- ✅ No unnecessary dependencies added
- ✅ Code is efficient and maintainable

## 📚 Documentation

When contributing:
- Update README.md if adding/changing features
- Add inline comments for complex code
- Update API documentation if modifying endpoints
- Add usage examples for new features

## 🚀 Release Process

Versions follow Semantic Versioning: MAJOR.MINOR.PATCH

- **MAJOR**: Incompatible API changes
- **MINOR**: New functionality, backward compatible
- **PATCH**: Bug fixes

## ❓ Questions?

Contact the developer:
- 📧 Email: nidhikumari934181@gmail.com
- 💼 LinkedIn: linkedin.com/in/nidhi-kumari-4648692b2
- 💻 GitHub: github.com/nidhikumari30

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing! Your efforts help make this project better for everyone! 🙌
