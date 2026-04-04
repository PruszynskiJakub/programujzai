# Lessons from Building Claude Code: How We Use Skills

![[00-Załączniki/Lessons from Building Claude Code How We Use Skills/08b97e8c24527cb52077b0290169b58d_MD5.jpg]]

## Metadata
- Author: [[Thariq]]
- Full Title: Lessons from Building Claude Code: How We Use Skills
- Category: #tweets
- Document Tags: [[favorite]] 
- Summary: Skills in Claude Code are powerful tools that help automate tasks using code, scripts, and dynamic configurations. They can be shared, combined, and measured to improve development efficiency across teams. Writing good skills means focusing on useful knowledge, organizing files clearly, and avoiding overly strict instructions.
- URL: https://x.com/trq212/status/2033949937936085378

## Full Document
[[Full Document Contents/Tweets/Lessons from Building Claude Code How We Use Skills.md|See full document content →]]

## Highlights
- Skills have become one of the most used extension points in Claude Code. They’re flexible, easy to make, and simple to distribute.
  But this flexibility also makes it hard to know what works best. What type of skills are worth making? What's the secret to writing a good skill? When do you share them with others?
  We've been using skills in Claude Code extensively at Anthropic with hundreds of them in active use. These are the lessons we've learned about using skills to accelerate our development. ([View Highlight](https://read.readwise.io/read/01km165ay4k4njzbh8jqy51bph))
    - Note: Skills są kluczowym rozszerzeniem Claude Code
- Types of Skills ([View Highlight](https://read.readwise.io/read/01km16qz22whz8hdvgvhmfk6ew))
- If you’re new to skills, I’d recommend [reading our docs](https://code.claude.com/docs/en/skills) or watching our newest course on [new Skilljar on Agent Skills](https://anthropic.skilljar.com/introduction-to-agent-skills), this post will assume you already have some familiarity with skills.
  A common misconception we hear about skills is that they are “just markdown files”, but the most interesting part of skills is that they’re not just text files. They’re folders that can include scripts, assets, data, etc. that the agent can discover, explore and manipulate.
  In Claude Code, skills also have a [wide variety of configuration options](https://code.claude.com/docs/en/skills#frontmatter-reference) including registering dynamic hooks.
  We’ve found that some of the most interesting skills in Claude Code use these configuration options and folder structure creatively. ([View Highlight](https://read.readwise.io/read/01km167weya7ddkym5k6znty6w))
    - Note: Skille to foldery, opakowujące złożone procesy w przystępnej konfigurowalnej formie.
- After cataloging all of our skills, we noticed they cluster into a few recurring categories. The best skills fit cleanly into one; the more confusing ones straddle several. This isn't a definitive list, but it is a good way to think about if you're missing any inside of your org. ([View Highlight](https://read.readwise.io/read/01km16e80ddvc1jh648z5mwz0y))
    - Note: Skille to mini samowystarczalne usługi, gotowe do użycia przez Claude Code.
      Istnieją clustry usług wokół których powstaje najwięcej skilli.
- **1. Library & API Reference**
  Skills that explain how to correctly use a library, CLI, or SDKs. These could be both for internal libraries or common libraries that Claude Code sometimes has trouble with. These skills often included a folder of reference code snippets and a list of gotchas for Claude to avoid when writing a script.
  **Examples:**
  • billing-lib — your internal billing library: edge cases, footguns, etc.
  • internal-platform-cli — every subcommand of your internal CLI wrapper with examples on when to use them
  • frontend-design — make Claude better at your design system ([View Highlight](https://read.readwise.io/read/01km16qs6dbrt1gehzykh8x7dd))
    - Note: Skille stanowiące usługi dla Claude Code w postaci samowystarczalnych folderów występują w otoczeniu pewnych określonych grup tematów.
      Jednym z tematów jest dostarczenie referencji i przykładów dla bibliotek.
- **2. Product Verification**
  Skills that describe how to test or verify that your code is working. These are often paired with an external tool like playwright, tmux, etc. for doing the verification.
  Verification skills are extremely useful for ensuring Claude's output is correct. It can be worth having an engineer spend a week just making your verification skills excellent.
  Consider techniques like having Claude record a video of its output so you can see exactly what it tested, or enforcing programmatic assertions on state at each step. These are often done by including a variety of scripts in the skill.
  **Examples:**
  • signup-flow-driver — runs through signup → email verify → onboarding in a headless browser, with hooks for asserting state at each step
  • checkout-verifier — drives the checkout UI with Stripe test cards, verifies the invoice actually lands in the right state
  • tmux-cli-driver — for interactive CLI testing where the thing you're verifying needs a TTY ([View Highlight](https://read.readwise.io/read/01km16wxgdzf4rga83nt4y5mya))
