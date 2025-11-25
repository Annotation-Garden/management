# Contributing to Annotation Garden


> [!WARNING] 
> **Draft** - This documentation is under development.

Thank you for your interest in contributing to the Annotation Garden Initiative! This document provides guidelines for contributing across all AGI repositories.

## Quick Start

```bash
# Clone the repository you want to contribute to
git clone https://github.com/Annotation-Garden/<repo-name>.git
cd <repo-name>

# Create a feature branch
git checkout -b feature/your-feature-name

# Make changes, test, and commit
git add .
git commit -m "Add your descriptive commit message"

# Push and create PR
git push -u origin feature/your-feature-name
```

## General Principles

1. **Open Science**: All contributions should advance open, reproducible science
2. **Standards Compliance**: Follow BIDS and HED specifications
3. **Version Control**: Use atomic commits and descriptive commit messages
4. **Collaboration**: Engage in discussions through Issues and PRs

## Contribution Workflow

### For Annotations

1. Fork the relevant stimulus repository
2. Add or refine annotations following the repository structure
3. Ensure HED validation passes (automated checks)
4. Submit a pull request with clear description of changes
5. Engage in review discussion

### For Code

1. Create a feature branch from main
2. Make changes with atomic commits
3. Test thoroughly before submitting PR
4. Follow code style guidelines (see specific repository)
5. Update documentation as needed

### For Documentation

1. Check for existing issues or discussions
2. Submit PRs for significant changes
3. Use clear, concise language
4. Include examples where helpful

## Commit Message Guidelines

- Use present tense ("Add feature" not "Added feature")
- Be concise but descriptive
- Reference issues when applicable (#123)
- No emojis in commit messages

## Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Assume good intentions
- Focus on scientific merit

## Contributing Across Multiple AGI Repositories

The Annotation Garden Initiative spans multiple repositories. Here are best practices for contributing across the organization:

### Getting Started

1. **Organization Repository**: Start in the [management](https://github.com/Annotation-Garden/management) repository for high-level discussions, governance questions, and cross-repository coordination
2. **Repository-Specific Work**: Move to specific repositories (stimulus datasets, tools, website, assets) for detailed work
3. **Stay Connected**: Reference management repository issues for context on organization-wide decisions

### Cross-Repository Coordination

- For changes affecting multiple repositories, discuss in the management repository first
- Coordinate with the Standards Working Group for BIDS/HED integration changes
- Reference related issues in dependent repositories using GitHub's linking syntax

### Linking Between Repositories

When making contributions that span multiple repositories:
1. Start with an issue in the management repository describing the cross-repository change
2. Create linked issues in each affected repository
3. Reference the management issue in PRs for traceability
4. Example: "See Annotation-Garden/management#123 for context"

## Development Setup

### Image Annotation Tool

```bash
# Backend (Python)
cd image-annotation
pip install -e .
pytest tests/ --cov

# Frontend (Next.js)
cd frontend
npm install
npm run dev
```

### Website

```bash
cd website
npm install
npm run dev
```

### Running Tests

Each repository has its own testing setup. Generally:
- Python: `pytest tests/ --cov`
- TypeScript/JavaScript: `npm test`

## Questions?

Open an issue in the relevant repository or the [management repository](https://github.com/Annotation-Garden/management) for general questions about AGI coordination and governance.
