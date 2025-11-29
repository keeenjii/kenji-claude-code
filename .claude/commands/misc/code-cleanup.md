---
description: Refactor and clean up code following best practices
model: claude-sonnet-4-5
---

Clean up and refactor the following code to improve readability, maintainability, and follow best practices.

## Code to Clean

$ARGUMENTS

## Cleanup Checklist for Solo Developers

### 1. **Code Smells to Fix**

**Naming**
-  Descriptive variable/function names
-  Consistent naming conventions (camelCase, PascalCase)
-  Avoid abbreviations unless obvious
-  Boolean names start with is/has/can

**Functions**
-  Single responsibility per function
-  Keep functions small (<50 lines)
-  Reduce parameters (max 3-4)
-  Extract complex logic
-  Avoid side effects where possible

**DRY (Don't Repeat Yourself)**
-  Extract repeated code to utilities
-  Create reusable components
-  Use TypeScript generics for type reuse
-  Centralize constants/configuration

**Complexity**
-  Reduce nested if statements
-  Replace complex conditions with functions
-  Use early returns
-  Simplify boolean logic

### 2. **Object Calisthenics Principles**
*(Apply when possible and when it improves code quality)*

**⚠️ Important:** These are guidelines, not strict rules. Apply them pragmatically when they genuinely improve the code. Some principles may not be applicable in every context.

1. **One Level of Indentation Per Method**
   - Extract nested logic into separate methods
   - Makes code more readable and testable
   - *Apply when:* You see multiple levels of nesting

2. **Don't Use the ELSE Keyword**
   - Use early returns instead
   - Reduces cognitive load
   - *Apply when:* It simplifies the logic flow

3. **Wrap All Primitives and Strings**
   - Create value objects for domain concepts
   - Adds type safety and semantic meaning
   - *Apply when:* The primitive has business meaning (e.g., Email, Money, UserId)

4. **First Class Collections**
   - Classes that contain a collection shouldn't contain other member variables
   - Encapsulate collection operations
   - *Apply when:* You have complex collection operations

5. **One Dot Per Line**
   - Avoid method chaining (Law of Demeter)
   - Reduces coupling between objects
   - *Apply when:* Long chains make code hard to understand or test

6. **Don't Abbreviate**
   - Use full, descriptive names
   - Code is read more than written
   - *Apply when:* Abbreviations are not universally understood

7. **Keep All Entities Small**
   - Classes: < 200 lines
   - Methods: < 15 lines
   - Packages: < 10 files
   - *Apply when:* A class/method is doing too many things

8. **No Classes With More Than Two Instance Variables**
   - Forces better decomposition
   - *Apply when:* It leads to better cohesion (this is the most debatable rule)

9. **No Getters/Setters/Properties**
   - Tell, don't ask
   - Objects should expose behavior, not data
   - *Apply when:* You can replace data access with meaningful methods

**Note:** Object Calisthenics are exercises to improve your coding skills. In production code, balance these principles with pragmatism, framework conventions, and team standards.
