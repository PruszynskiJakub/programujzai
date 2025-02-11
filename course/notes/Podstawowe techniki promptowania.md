---
tags:
  - prompt
  - todo
---
https://www.promptingguide.ai/

Here's a concise breakdown of these prompting techniques:

#### Zero-shot
- Direct question without examples
- "What's the capital of France?"
- Simplest but less accurate for complex tasks

#### Few-shot
- Provides 2-3 examples before the main task
- Shows pattern/format expected
- "Add 2+2=4, 3+3=6, now solve 5+5=?"

#### Chain of Thoughts (CoT)
- Breaks problem into step-by-step reasoning
- Shows working process, not just answer
- "Let's solve this step by step..."
- _reasoning property

#### Zero-shot CoT
- No examples but prompts for reasoning
- Uses triggers like "Let's think about this logically"
- "Let's solve this step by step, first..."
- _reasoning property

#### Few-shot CoT
- Combines examples with reasoning steps
- Shows both pattern and thought process
- Most effective but verbose
- "Example: 15+17? Step 1: Add tens (10+10=20), Step 2..."
- _reasoning property