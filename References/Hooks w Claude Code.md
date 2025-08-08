---
tags:
  - references
category:
  - "[[Technique]]"
  - "[[Tool Skill]]"
url:
  - https://docs.anthropic.com/en/docs/claude-code/hooks
---
Jest to jedna z funkcjonalności, technik współpracy z [[Claude Code]] pozwalająca na automatyczne odpalanie komend powłoki w różnych momentach działania narzędzia. Dzięki nim pewne zachowania stają się deterministyczne bez polegania na LLM.

## Practical Applications

Here are some common ways to use hooks:

- **Code formatting** - Automatically format files after Claude edits them
- **Testing** - Run tests automatically when files are changed
- **Access control** - Block Claude from reading or editing specific files
- **Code quality** - Run linters or type checkers and provide feedback to Claude
- **Logging** - Track what files Claude accesses or modifies
- **Validation** - Check naming conventions or coding standards

The key insight is that hooks let you extend Claude Code's capabilities by integrating your own tools and processes into the workflow. PreToolUse hooks give you control over what Claude can do, while PostToolUse hooks let you enhance what Claude has done.

### PreToolUse
Zwraca exit code 0 jeśli wszystko okay
Zwraca exit code 2 jeśli chcemy zablokować tool


[[Attachments/Hooks w Claude Code/9e3d40560663bb6388110c33e954e37a_MD5.jpeg|Open: Screenshot 2025-07-23 at 09.42.57.png]]
![[Attachments/Hooks w Claude Code/9e3d40560663bb6388110c33e954e37a_MD5.jpeg]]

#### Summary

Claude Code hooks can help address common weaknesses in AI-assisted development, particularly on larger projects. These hooks run automatically when Claude makes changes to your code, providing immediate feedback and preventing common issues.

## TypeScript Type Checking Hook

One of the most useful hooks addresses a fundamental problem: when Claude modifies a function signature, it often doesn't update all the places where that function is called throughout your project.

For example, if you ask Claude to add a `verbose` parameter to a function in `schema.ts`, it will successfully update the function definition but miss the call site in `main.ts`. This creates type errors that Claude doesn't immediately catch.

The solution is a post-tool-use hook that runs the TypeScript compiler after every file edit:

- Runs `tsc --noEmit` to check for type errors
- Captures any errors found
- Feeds the errors back to Claude immediately
- Prompts Claude to fix the issues in other files

This hook works for any typed language where you can run a type checker. For untyped languages, you could implement similar functionality using automated tests instead.

## Query Duplication Prevention Hook

In larger projects with many database queries, Claude sometimes creates duplicate functionality instead of reusing existing code. This is especially problematic when you give Claude complex, multi-step tasks that include database operations as just one component.

Consider a project structure with multiple query files, each containing many SQL functions. When you ask Claude to "create a Slack integration that alerts about orders pending longer than 3 days," it might write a new query instead of using the existing `getPendingOrders()` function.

![[Attachments/Hooks w Claude Code/a0a044bd6253f4559b1e95690d630655_MD5.png]]

The query duplication hook addresses this by implementing a review process:

![[Attachments/Hooks w Claude Code/05e32db8e02ed545bc6ea49419cfe906_MD5.png]]

Here's how it works:

- Triggers when Claude modifies files in the `./queries` directory
- Launches a separate instance of Claude Code programmatically
- Asks the second instance to review the changes and check for similar existing queries
- If duplicates are found, provides feedback to the original Claude instance
- Prompts Claude to remove the duplicate and use the existing functionality

## Implementation Considerations

Both hooks use the pre-tool-use or post-tool-use hook system. The TypeScript hook is relatively lightweight and runs quickly. The query duplication hook requires more resources since it launches a separate Claude instance for each review.

For the query hook, consider these trade-offs:

- **Benefits:** Cleaner codebase with less duplication
- **Costs:** Additional time and API usage for each query directory edit
- **Recommendation:** Only monitor critical directories to minimize overhead

The hooks use Claude's TypeScript SDK to programmatically interact with the AI. This allows you to create sophisticated workflows where one Claude instance can review and provide feedback on another's work.

## Extending These Concepts

These hooks demonstrate broader principles you can apply to your own projects:

- Use compiler/linter output to provide immediate feedback
- Implement code review processes using separate AI instances
- Focus monitoring on high-value directories where consistency matters most
- Balance automation benefits against performance costs

The key is identifying the specific pain points in your development workflow and creating targeted hooks that address those issues automatically.

[

](https://anthropic.skilljar.com/claude-code-in-action/312423 "Gotchas around hooks")