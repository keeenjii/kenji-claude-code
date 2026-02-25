# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.


## Development Guidelines

### Planning and Problem-Solving Approach

**CRITICAL: Graph-Based Thinking - No Linear Planning**

When planning, architecting, or problem-solving, you MUST use graph/flowchart structures instead of linear bullet points.

**Requirements:**
- **No simple bullet lists** - Linear lists hide dependencies, failure states, and branches
- **Use Node-and-Edge structure** - Think in terms of flowcharts with decision points
- **Include Decision Diamonds** - Every step must consider: "What if this fails? What are the alternatives?"
- **Identify failure states** - Map out dead ends, error paths, and recovery loops
- **Show dependencies** - Make explicit what depends on what
- **Format for diagramming** - Structure output so it can be visualized in a flowchart tool

**Example Structure:**
```
START → [Check if service exists]
  ├─ YES → [Verify configuration]
  │   ├─ VALID → [Deploy service]
  │   │   ├─ SUCCESS → END
  │   │   └─ FAIL → [Rollback] → [Log error] → END
  │   └─ INVALID → [Show validation errors] → [Fix configuration?]
  │       ├─ YES → LOOP to [Verify configuration]
  │       └─ NO → END
  └─ NO → [Create new service] → [Verify configuration]
```

**Why this matters:**
- Prevents "happy path" bias where plans assume everything works perfectly
- Forces consideration of error handling, edge cases, and dependencies
- Produces more robust, production-ready solutions
- Makes plans easier to review and debug

### Code Quality Standards
- **SOLID Principles**: Always follow Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion principles
- **Object Calisthenics**: Apply object-oriented best practices including proper encapsulation, meaningful naming, and minimal method complexity
- After every major change, run build comand to check for errors and fix then
- Avoid creating too much docs (.md) files. Only create then when explicity asked