---
layout: post
subtitle: Exploring different approaches to AI integration in a real-world insurance claim processing scenario
title: "AI Hackathon: Building the Future of Software Engineering"
date: 2025-05-14 08:00:00 -0400
categories: [Artificial Intelligence, Hackathon, Software Engineering]
tags: [Artificial Intelligence, Hackathon, Software Engineering, Innovation]
comments: true
social-share: true
thumbnail-img: /assets/img/human-ai.png
---

Last week, I participated in an internal AI hackathon at Centric Consulting, focused on building an AI-powered insurance claim triage system. The challenge was based on a fictional scenario involving Censurance, a hypothetical insurance company. The hackathon brought together developers, engineers, and AI enthusiasts from across our organization to tackle a real-world challenge in insurance claim processing.

### The Challenge

The hackathon centered on building an AI-powered API that could revolutionize how insurance claims are processed. In our fictional scenario, it takes Censurance staff 2-3 days to review each claim manually, causing customer frustration and leaving room for undetected fraud. Teams were tasked with building a proof-of-concept API that could:

- Classify claims into categories (Urgent, Routine, Potential Fraud, or Needs More Information)
- Provide AI-generated rationales for each classification
- Include confidence scores and metadata for logging
- Handle edge cases and ambiguous claims
- Implement semantic logging for transparency

### Team Approaches

The hackathon featured three distinct approaches:

1. **Low-Code/No-Code Solution**: One team used a low-code approach, creating a Model-Controller-Provider (MCP) server with an agent workflow. An MCP server is a lightweight web server that handles model interactions, request routing, and data provisioning. This solution showed how AI can be integrated into existing systems with minimal traditional coding.

2. **.NET API with GitHub Copilot**: Another team built a .NET API, using GitHub Copilot to accelerate development. They integrated Microsoft's Semantic Kernel with an AI model to process and classify claims.

3. **Agent C Platform**: The third team used our [Agent C Framework](https://github.com/centricconsulting/agent_c_framework), an open-source framework for building interactive, tool-using AI agents. Agent C provides a runtime environment that handles streaming responses, parallel tool execution, and asynchronous operations. The team leveraged these capabilities to create a robust claim processing system that could handle multiple claims simultaneously while maintaining clear audit trails of the AI's decision-making process.

### Quality Assurance

The hackathon emphasized both solution quality and business effectiveness. Teams focused on four key areas:

1. **Software Quality**: Testing, security, and code maintainability
2. **Solution Validation**: Classification accuracy and decision transparency
3. **Business Requirements**: Processing time reduction and fraud detection
4. **Cost Optimization**: Token usage and model efficiency

This focus ensured that solutions were both technically sound and valuable for the business case. Teams balanced AI response quality with associated costs, ensuring that automation benefits outweighed implementation expenses.

### Key Learnings

The hackathon provided several insights:

1. **AI Integration**: We learned how to integrate AI models into development workflows
2. **Team Collaboration**: Working with diverse skill sets helped us approach problems from different angles
3. **Rapid Prototyping**: The time constraint forced us to focus on core functionality and iterate quickly
4. **Future of Development**: We gained a deeper understanding of how AI will shape software engineering

### Resources

For those interested in building similar AI-powered solutions, here are some helpful resources:

- [Azure OpenAI Service Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/)
- [Semantic Kernel Framework](https://learn.microsoft.com/en-us/semantic-kernel/)
- [OpenTelemetry for Observability](https://opentelemetry.io/)
- [.NET Aspire Dashboard](https://learn.microsoft.com/dotnet/aspire/fundamentals/dashboard/standalone)
- [Agent C Framework](https://github.com/centricconsulting/agent_c_framework) - An open-source framework for building interactive, tool-using AI agents

### Finally

The AI Hackathon demonstrated the potential of AI in transforming business processes. As we continue to explore this space, I'm excited to see how these innovations will transform not just software engineering, but entire industries like insurance.

What are your thoughts on the role of AI in transforming traditional industries? Have you participated in any similar hackathons? Share your experiences in the comments below. 