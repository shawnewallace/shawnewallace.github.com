---
layout: post
subtitle: A curated collection of AI assistant prompts, instructions, and configurations organized by development scenario
title: "Building a Personal Prompt Library: Enhancing Your AI Development Workflow"
date: 2025-11-19 08:00:00 -0400
categories: [Artificial Intelligence, Software Engineering]
tags: [Artificial Intelligence, Software Engineering, Prompt Engineering, Developer Tools, Productivity]
comments: true
social-share: true
thumbnail-img: /assets/img/prompt-library-hero.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

## Introduction

As AI-powered development tools like GitHub Copilot and Claude Code become integral to our daily workflows, I've found that the quality of our interactions with these tools directly impacts our productivity. Rather than starting from scratch with every project or relying on generic prompts, I've been building a structured prompt library to help configure AI assistants for specific development scenarios. Today, I'm excited to share this [prompt library repository](https://github.com/shawnewallace/prompt-library) and the thinking behind it.

## Why Build a Prompt Library?

Even after collecting just a handful of effective prompts, I quickly realized I was facing a new problem: I kept retyping the same instructions across different projects and AI tools. A code review prompt that worked well in one repository needed to be manually copied to another. A debugging template I refined for Python needed the same adjustments when I used it for TypeScript. The same architectural guidance kept appearing in multiple project configurations.

The need for aggregation and reuse became obvious almost immediately. Rather than scattering effective prompts across chat histories, project files, and personal notes, a structured library solves this problem by providing:

1. **Consistent Context Across Projects**: Define once, reuse everywhere
2. **Scenario-Specific Guidance**: Different projects need different approaches
3. **Team Alignment**: Share prompts to ensure everyone follows the same patterns
4. **Continuous Improvement**: Refine prompts based on real-world results
5. **Knowledge Preservation**: Capture best practices as they emerge

What started as a simple collection of a few prompts naturally evolved into a structured system once I recognized this pattern: the prompts I found most valuable were the ones I needed to use repeatedly.

## Structure and Organization

The library is organized around development scenarios rather than tools, making it easier to find relevant prompts regardless of which AI assistant you're using:

```
prompt-library/
├── scenarios/          # Scenario-specific resources
├── shared/            # Cross-scenario resources
└── examples/          # Real-world usage examples
```

### Current Scenarios

The library currently includes four primary scenarios that cover most of my development work:

#### 1. .NET Clean Architecture
Prompts and configurations for building enterprise .NET applications following Clean Architecture principles, Domain-Driven Design, and SOLID patterns. This scenario is particularly useful when:
- Building enterprise applications with complex business logic
- Implementing DDD aggregates and entities
- Following Clean Architecture layering
- Writing comprehensive unit tests with TDD

#### 2. Python Data Science
Resources tailored for data analysis, machine learning, and scientific computing projects. Use this scenario when:
- Working with pandas, numpy, and scikit-learn
- Building ML models and pipelines
- Performing data exploration and visualization
- Developing in Jupyter notebooks

#### 3. TypeScript Frontend
Tools for modern frontend development with JavaScript/TypeScript frameworks. This scenario helps with:
- Building React, Vue, or Angular applications
- Working with TypeScript type systems
- Component development and testing
- State management and API integration

#### 4. DevOps Infrastructure
Prompts focused on infrastructure as code, CI/CD, and deployment automation:
- Writing Terraform, CloudFormation, or other IaC
- Setting up CI/CD pipelines
- Container and Kubernetes configuration
- Deployment and monitoring scripts

### Shared Resources

The `shared/` directory contains general-purpose resources that apply across scenarios:
- **prompts/**: Common tasks like code review, debugging, and documentation
- **templates/**: Reusable prompt templates for standardization
- **snippets/**: Frequently used prompt fragments

## Quick Start: Common Prompts

For those just getting started with prompt engineering, I've included several ready-to-use prompts for everyday development tasks:

### Code Review Prompt
```
Review the following code for:
- Code quality and readability
- Best practices and design patterns
- Potential bugs or edge cases
- Performance considerations
- Security vulnerabilities
- Test coverage gaps

[Paste your code here]
```

### Debugging Prompt
```
I'm encountering the following issue:

**Problem:** [Describe the bug/error]
**Expected behavior:** [What should happen]
**Actual behavior:** [What's actually happening]
**Error messages:** [Any error output]

**Code:**
[Paste relevant code]

**Context:**
[Environment, dependencies, recent changes]

Please help me:
1. Identify the root cause
2. Suggest a fix
3. Explain why this is happening
4. Recommend how to prevent similar issues
```

These templates provide structure while remaining flexible enough to adapt to specific situations.

## Tool-Specific Configurations

The library includes configurations for both Claude Code and GitHub Copilot:

### For Claude Code
Copy instructions from `scenarios/{scenario}/claude-code/instructions.md` to your Claude Code configuration, or use slash commands from the `commands/` folder for quick access to specific functionality.

### For GitHub Copilot
Copy content from `scenarios/{scenario}/github-copilot/instructions.md` to `.github/copilot-instructions.md` in your project root. This provides project-specific context to Copilot across your entire team.

## Real-World Impact

Since building this library, I've noticed several improvements in my AI-assisted development workflow:

**Faster Onboarding**: When starting a new project, I can quickly configure my AI assistant with the appropriate scenario, eliminating the need to repeatedly explain architectural patterns or coding standards.

**Better Code Quality**: Scenario-specific prompts that emphasize best practices have led to more consistent, higher-quality code suggestions that align with established patterns.

**Reduced Context Switching**: Having predefined prompts for common tasks (code review, debugging, documentation) means less time crafting the perfect prompt and more time actually developing.

**Team Consistency**: When working with colleagues, sharing scenario configurations ensures everyone's AI assistant provides suggestions that align with team standards.

## "Stealing" and Adapting Prompts

One of the most valuable aspects of building this library has been collecting and adapting prompts I encounter in the wild. I'm constantly "stealing" effective prompts from:

- **Colleagues**: When someone shares a particularly effective prompt during pair programming or code reviews, I add it to the library
- **Online Communities**: Blog posts, GitHub repositories, and developer forums are goldmines for well-crafted prompts
- **AI Tool Documentation**: Official guides often contain gems that work better than my initial attempts
- **Trial and Error**: Sometimes the best prompts come from iterating on something I found elsewhere

The key is treating found prompts as starting points rather than final products. I adapt them to:
- Match my specific development context and patterns
- Align with team conventions and standards  
- Work across multiple AI tools in my workflow
- Fit the structure of my scenario-based organization

This "collect, adapt, refine" approach means I'm building on the community's collective wisdom rather than reinventing the wheel. Every prompt in the library represents the best version of something I've tried, whether I wrote it from scratch or adapted it from somewhere else.

## The Broader Ecosystem

This library stands on the shoulders of some excellent community resources. I've been inspired by and learned from:

- [Anthropic Prompt Library](https://docs.anthropic.com/claude/prompt-library) - Official collection for Claude
- [GitHub Copilot Patterns](https://github.blog/developer-skills/github/how-to-write-better-prompts-for-github-copilot/) - Best practices for Copilot
- [Cursor Rules](https://github.com/pontusab/cursor.directory) - Community-sourced rules for Cursor IDE
- [Prompt Engineering Guide](https://www.promptingguide.ai/) - Comprehensive guide to prompt engineering

These resources provide broader coverage and different perspectives that complement the scenario-focused approach in my library.

## Looking Forward

This prompt library is a living project that evolves with my development practices and the AI tools themselves. I'm planning to add:

- Additional scenarios (mobile development, embedded systems, etc.)
- More advanced agent definitions and workflows
- Team collaboration patterns and examples
- Integration guides for additional AI tools

## Get Started

The [prompt-library repository](https://github.com/shawnewallace/prompt-library) is available on GitHub for anyone to use and adapt. Whether you're working with Claude Code, GitHub Copilot, or other AI development tools, I hope you'll find value in the structured approach to prompt engineering.

I encourage you to:
1. Explore the repository and try the scenarios that match your work
2. Adapt the prompts to your specific needs and team standards
3. Share feedback or contribute improvements

## Contributing to the Library

This prompt library is designed to be a community resource, and contributions are welcome. Whether you've refined an existing prompt, discovered a new pattern, or built out an entirely new scenario, your experience can help others.

### Ways to Contribute

**Share Your Prompts**: If you've developed prompts that work well for your workflow, consider contributing them back. The most valuable contributions often come from real-world usage and iteration.

**Add New Scenarios**: Working in a domain not yet covered? Mobile development, game development, embedded systems, and many other specializations would benefit from dedicated scenarios.

**Improve Documentation**: Clear examples and usage guides make prompts more accessible. If you've found a particularly effective way to use a prompt, document it.

**Report What Works (and What Doesn't)**: Feedback on prompt effectiveness helps everyone. If a prompt produces consistently good results or needs refinement, that information is valuable.

### Contribution Guidelines

When contributing to the library:

1. **Follow the Structure**: Place scenario-specific content in the appropriate `scenarios/{scenario}/` directory, and cross-cutting resources in `shared/`
2. **Document Usage**: Include clear examples showing when and how to use the prompt
3. **Test Your Prompts**: Verify prompts work with the tools you're targeting (Claude Code, GitHub Copilot, etc.)
4. **Explain Adaptations**: If you've adapted a prompt from elsewhere, note what you changed and why
5. **Keep It Practical**: Focus on prompts that solve real development challenges

The goal is to build a collection that's immediately useful to developers while remaining easy to maintain and extend. Even small contributions—fixing typos, clarifying instructions, or sharing a single effective prompt—help improve the library for everyone.

## Conclusion

As AI-powered development tools continue to mature, the ability to effectively communicate with these assistants becomes increasingly important. A well-organized prompt library isn't just about saving time—it's about establishing a systematic approach to AI collaboration that improves over time.

By treating prompt engineering as a first-class development practice, with version control, documentation, and continuous refinement, we can unlock the full potential of AI-assisted development while maintaining the quality and consistency our projects demand.

What prompts or scenarios would you add to a library like this? I'd love to hear about the patterns and practices that work best in your development workflow.
