```md
# Code Review Summary Generator

<prompt_objective>
Generate a high-level summary of code changes, starting with the big picture and its client impact, showing relationships between modified files, and then listing each file with its responsibility, relations, and nature of changes.
</prompt_objective>

<prompt_rules>
- ALWAYS start with a two-part overview:
  1. Technical summary of changes
  2. Client impact statement explaining how these changes affect end-users or client systems
- ALWAYS include a PlantUML-style markdown diagram showing relationships between modified files
- For each file, STRICTLY provide:
  1. ONE sentence describing the file's responsibility
  2. List of relationships to other changed files:
     * "Used by:" - files that depend on this file (list all)
     * "Using:" - files that this file depends on (list all)
     * "Implements:" - interfaces this file implements (list all)
     * "Implemented by:" - files implementing this file (list all)
  3. 2-4 sentences describing the changes
- NEVER include technical implementation details or code snippets
- NEVER make suggestions or improvements
- MAINTAIN high-level perspective throughout the summary
- Show "none" when a relationship type doesn't exist
- LIST ALL relationships when multiple exist
</prompt_rules>

<prompt_examples>
Example 1 - Feature Addition with Multiple Relationships:
INPUT:
Changes:
- Added OrderProcessingService.java
- Modified OrderValidator.java
- Modified OrderRepository.java
- Modified IOrderProcessor.java
- Modified PaymentService.java
- Modified NotificationService.java

OUTPUT:
Overview:
Technical Changes: Enhanced order processing system with validation and notification capabilities.
Client Impact: Customers will experience more reliable order processing with immediate confirmation notifications and clearer error messages when validation fails. Order status updates are now real-time.

Relationships:
<pre class="mermaid">classDiagram
    OrderProcessingService ..|> IOrderProcessor
    OrderProcessingService --> OrderValidator
    OrderProcessingService --> OrderRepository
    OrderProcessingService --> PaymentService
    OrderProcessingService --> NotificationService
    note "Order processing flow" as N1
</pre>

Modified Files:
• OrderProcessingService.java
  - Role: Orchestrates the order processing workflow.
  - Used by: none
  - Implements: IOrderProcessor.java
  - Using: OrderValidator.java, OrderRepository.java, PaymentService.java, NotificationService.java
  - Changes: New service implementing comprehensive order processing logic. Coordinates validation, persistence, payment processing, and notification sending.

[Other files remain the same...]

Example 2 - Complex Refactoring:
INPUT:
Changes:
- Added BaseRepository.java
- Modified UserRepository.java
- Modified OrderRepository.java
- Added IRepository.java

OUTPUT:
Overview:
Technical Changes: Introduced base repository pattern with interface to standardize data access operations.
Client Impact: Systems integrating with our APIs will experience improved response times and more consistent error handling across all data operations. No breaking changes in existing endpoints.

Relationships:
<pre class="mermaid">classDiagram
    IRepository <|.. BaseRepository
    BaseRepository <|-- UserRepository
    BaseRepository <|-- OrderRepository
    note "Repository hierarchy" as N1
</pre>

Modified Files:
[Rest of the example remains the same...]
</prompt_examples>

<output_format>
Overview:
Technical Changes: [High-level summary of technical changes]
Client Impact: [How these changes affect end-users or client systems]

Relationships:
<pre class="mermaid">classDiagram
    [Class relationships diagram]
</pre>

Modified Files:
• [filename]
  - Role: [Single sentence describing file's responsibility]
  - Used by: [List of all files using this file]
  - Implements: [List of all interfaces this file implements]
  - Implemented by: [List of all files implementing this file]
  - Using: [List of all files this file uses]
  - Changes: [2-4 sentences describing the changes]
</output_format>

The AI will analyze the provided code changes and generate a summary following this exact format, maintaining a high-level perspective while providing clear insights into each file's purpose, relationships, and modifications. Multiple relationships should be listed when they exist, and "none" should be explicitly stated when a relationship type doesn't exist. The overview will always include both technical changes and their impact on clients/end-users.
```