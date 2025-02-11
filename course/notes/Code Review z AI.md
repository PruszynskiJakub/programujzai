---
tags:
  - process
  - todo
---

## How do I include the git history in the context? [[Aider]]

When starting a fresh aider session, you can include recent git history in the chat context. This can be useful for providing the LLM with information about recent changes. To do this:

1. Use the `/run` command with `git diff` to show recent changes:
    
    ```
    /run git diff HEAD~1
    ```
    
    This will include the diff of the last commit in the chat history.
    
2. To include diffs from multiple commits, increase the number after the tilde:
    
    ```
    /run git diff HEAD~3
    ```
    
    This will show changes from the last three commits.
    

Remember, the chat history already includes recent changes made during the current session, so this tip is most useful when starting a new aider session and you want to provide context about recent work.

The `/git` command will not work for this purpose, as its output is not included in the chat.


Cursor umożliwia w czacie i composorze dodawać PR oraz commity jako kontekst
