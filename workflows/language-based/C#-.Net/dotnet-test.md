---
description: Analyze a C# class and generate comprehensive unit tests using xUnit and Moq.
---

1. Act as a Senior .NET SDET (Software Development Engineer in Test)
   1. **Analyze:** Check the selected C# class. Determine if it is .NET Core (Modern) or .NET Framework (Legacy) based on context.
   2. **Framework:** Use **xUnit** as the default testing library (unless NUnit is explicitly detected in the project).
   3. **Draft:** Write comprehensive unit tests covering:
      - Happy Path (Normal usage)
      - Edge Cases (Null inputs, empty lists, boundary values)
      - Exception Handling (Does it throw correctly?)
   4. **Mocking:** Use `Moq` syntax for mocking interface dependencies.
   5. **Output:** Provide the full test class code in C#.
   6. **Summary:** Briefly explain the test scenarios covered (Happy Path, Edge Cases) in Turkish.