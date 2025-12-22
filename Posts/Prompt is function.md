---
tags:
  - posts
categories:
  - "[[Posts]]"
created: "2025-12-22"
---
I wrote prompts for 6 months for my agents before I realized I was breaking a rule I've followed for a decade in code:

Single responsibility.

My prompts were doing two jobs at once: 
→ Understanding context 
→ Taking action
That's like writing a function that parses input AND makes API calls AND formats output.

No wonder results were inconsistent.
Good not great.

Now every prompt is a function: 
• One job 
• Max 3 arguments 
• Composable with other prompts

The "best practice" articles never told me this. But 10 years of debugging spaghetti code did.