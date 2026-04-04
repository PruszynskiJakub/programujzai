# Slow Down to Speed Up

![[00-Załączniki/Slow Down to Speed Up/d5c95a75f006037c6f371644ad55890a_MD5.jpg]]

## Metadata
- Author: [[James Stanier]]
- Full Title: Slow Down to Speed Up
- Category: #articles
- Summary: AI can make coding faster but also spreads mistakes quickly if we rush without clear plans. Slowing down to think carefully about goals and problems before using AI leads to better results. Using AI to help both plan and build can save time and improve quality in the long run.
- URL: https://theengineeringmanager.substack.com/p/slow-down-to-speed-up?utm_source=unknownews

## Full Document
[[Full Document Contents/Articles/Slow Down to Speed Up.md|See full document content →]]

## Highlights
- When slowness pays off ([View Highlight](https://read.readwise.io/read/01km7vtvjk2hgyap56de55sfgc))
    - Note: Myślenie przed działaniem, planowanie przed implementacją, a nie naiwny bieg bez kierunku. W obszarze planowania i analizy dobre praktyki są skuteczne.
- This month, we’re going to explore what might be the most counterintuitive practice in the age of AI: knowing when to *slow down*.
  Hang on, slow down? Yes, bear with me here.
  Let’s bring the debate that’s probably been going on in your team for some time to a head. Some of your colleagues say that with AI we should be building and shipping even faster, prototyping in hours, and that perhaps we don’t even need to write code at all any more: we should just let the models go full auto. They’re just *that* good now.
  Others worry that this speed is creating quality problems, that we’re accumulating technical debt faster than we can pay it down, and that codebases are becoming patchworks of AI slop that nobody fully understands. ([View Highlight](https://read.readwise.io/read/01km7t89z5rzt3ntn9khemjq8s))
    - Note: Wokół AI widać dwie frakcję jedyna mówi róbmy wszystko szybciej, druga martwi się o jakość stojąc lekko w kontrze.
- We’ll start by looking at this debate through the lens of Daniel Kahneman’s System 1 and System 2 thinking, and why AI has made the slow phases of work *more* important, not less. Then we’ll examine the illusion of speed: the thought process around rework costs, and why going fast in the wrong phase means going slow overall. ([View Highlight](https://read.readwise.io/read/01km7teqj56wx7gneq1jfqcxh1))
    - Note: Kluczowe pytanie o szybkość pracy z AI to Kiedy a nie czy.
- There’s a useful way to frame the debate that we opened with. In his oft-cited *[Thinking, Fast and Slow](https://en.wikipedia.org/wiki/Thinking,_Fast_and_Slow)*, Daniel Kahneman describes two modes of thinking: one that’s fast, automatic, and pattern-matching, and another that’s slow, deliberate, and analytical.
  Transpose this thinking onto LLMs: in his [conversation with Dwarkesh Patel](https://www.dwarkesh.com/p/andrej-karpathy), Andrej Karpathy describes them as ghosts or spirits, a kind of statistical distillation of human text, ethereal entities that are fully digital and mimicking humans. Words go in, patterns get matched, and words come out, which is, if you think about it, essentially, System 1 thinking.
  AI is extraordinarily good at this kind of work: fast pattern-matching at scale. But the second kind of thinking, the work of deciding *what* to build, *why* it matters, and *whether* we’re solving the right problem, still requires human judgment. ([View Highlight](https://read.readwise.io/read/01km7twytjvarfx1xrn2erfsm8))
    - Note: Przy pracy z AI kluczowe jest wiedzieć kiedy i dlaczego działamy w konkretnym trybie. LLM są odpowiednikiem naszego systemu myślowego odpowiedzialnego za szybkie automatyczne rozpoznawanie wzorców.
- And here’s the counterintuitive and highly interesting part: AI didn’t make the slow phases less important, it made them *more* important. When execution is cheap and fast, the leverage shifts to the decisions that precede it.
  A wrong requirement, a misunderstood problem, a flawed design assumption: these propagate through everything AI helps you build, only now they propagate *faster*. The cost of getting System 2 wrong goes up precisely because System 1 has become so powerful.
  If we want to go fast, we need to slow down first. ([View Highlight](https://read.readwise.io/read/01km7v3cac3fyzya1xvm89w7ke))
    - Note: Ludzki umysł balansuje pomiędzy trybem szybkim, automatycznym oraz wolnym analitycznym. Praca z AI rezonuje z tym pierwszym , powodując dysproporcję pomiędzy tymi trybami, nadając wagi działaniu świadomemu w tym drugim.
- Back when I was doing my PhD, there was a common saying in academic circles: something like a few weeks in the lab will save you hours in the library. Software development has its own version: weeks of coding can save you hours of planning.
  The reason it’s a joke, of course, is that both are *backwards*: the rush to start, the mounting realisation that something fundamental is wrong, and the painful rework that follows. I’ve certainly done many software projects where I wish I’d stopped and thought a little more before I rushed in. I can feel the cold flush coming back to me that you get when you stare at weeks of work that are completely wrong.
  We have a clear intuition in software engineering that we should catch mistakes early, ideally in requirements or design, because the further a project moves on, the more expensive it is to fix them. Common sense can derive this without any research to back it up: a box diagram is easy to change, a misunderstood requirement less so, and a fundamentally flawed deployed architecture is a rewrite.
  Therefore, here’s the problem: AI can help you create technical debt faster than ever! Oh no! ([View Highlight](https://read.readwise.io/read/01km7vbaardeqahv812e61t01p))
    - Note: AI rezonuje z ludzkim szybkim automatycznym trybem myślenia wprowadzając nierównowagę z wolnym analitycznym myśleniem. Mimo podświadomego zrozumienia, że ten pierwszy musi być poprzedzony tym drugim, aby rezulat był trwały.
- If the decisions that precede execution are flawed, AI will faithfully implement those flaws in a way that looks like fully featured code. Looks can often be deceiving, especially with powerful and confident models. It will generate thousands of lines of code based on a misunderstood requirement. It will happily build an elegant solution to the wrong problem.
  The illusion of speed is that you’re making progress when you’re actually digging yourself into a deeper hole.
  The answer isn’t to abandon speed, but to deploy it *deliberately*. We should only unleash AI’s pace when we’re confident it’s pointed in the right direction. Which raises the question: how do we know when that is? ([View Highlight](https://read.readwise.io/read/01km7vj50mk9zva19tpt2p5ya6))
    - Note: Nasza praca powinna działać w równowadze pomiędzy metodycznym i wolnym planowaniem, a szybką automatyczną implementacją. Bez uważnego podejścia sami prowadzimy do nieprzyjemnych konsekwencji.
- The places where deliberate slowness pays off haven’t changed much, even as everything around them has accelerated. Requirements are still cheap to change when they’re just words on a page, and expensive when they’re deployed code serving real users. Design decisions are still easier to revise in a diagram than in a production system. AI didn’t alter this fundamental physics; it just increased the leverage of getting it right.
  In a previous article, I called this the *[thinking first](https://www.theengineeringmanager.com/growth/use-it-or-lose-it/)* [protocol](https://www.theengineeringmanager.com/growth/use-it-or-lose-it/): before offloading work to AI, spend time clarifying what you actually want. This isn’t unnecessary process; it’s the cheapest possible place to catch mistakes. ([View Highlight](https://read.readwise.io/read/01km7vttmmqv6pbf7ttrms43dy))
- Here is the interesting paradox which shows the incredible usefulness of AI: the same tool that accelerates execution can also accelerate deliberation. Here are some practical ways to do this:
  • **Clarify requirements before coding.** Spend 10 minutes writing down the problem you’re solving, your success criteria, and your [constraints](https://www.theengineeringmanager.com/growth/the-beauty-of-constraints/) before asking AI to generate anything. What does “done” look like? What’s out of scope? Then get AI to interrogate everything that you’ve written before generating.
  • **Run a pre-mortem.** Ask AI “What could go wrong with this approach?” before committing to a design. It will surface risks you hadn’t considered.
  • **Invert the problem.** Ask AI “What would make this project fail?” to expose hidden assumptions. I’ve written more about this technique in [Invert, always invert](https://www.theengineeringmanager.com/growth/invert-always-invert/).
  • **Build a throwaway prototype.** Use AI to create something in hours, show it to stakeholders, and validate your understanding before investing weeks. This is speed in service of slowness: you’re investing time upfront to learn.
  • **Build scrappy internal tools.** Before you spend money on real products, use AI to build your own rough versions first. You’ll learn what you actually need and what you don’t. If you’re a paid subscriber, last month’s article goes deeper into some of the tools I’ve built myself.
  • **Surface edge cases early.** Ask AI to generate edge cases and failure modes for your design before implementation begins. It’s far cheaper to handle them in a diagram than in production. ([View Highlight](https://read.readwise.io/read/01km7w05af1phz4ahzjsbyb8t5))
    - Note: Działanie powinno poprzedzać myślenie, dzięki temu outcome będzie satysfakcjonujący i trwały. Również w fazie myślenia AI może nas wesprzeć nie jako generator ale jako sparing partner.
- Given that AI is speeding things up so much, if you haven’t already been challenged on why something’s taking so long, you certainly will be soon.
  “Can’t you just use AI?” is a new form of velocity pressure, and it’s particularly insidious because it conflates the [appearance of productivity](https://www.theengineeringmanager.com/management-101/feeling-productive/) with actual throughput. Yes, AI can generate code in seconds. But generating code and solving the *right* problem are not the same thing.
  So, what do you do?
  • **Be explicit about which phase you’re in.** If you’re in the slow phase, say so: explain that you’re clarifying requirements, thinking through edge cases, and making sure you’re solving the right problem.
  • **Invite stakeholders to contribute.** Their input is cheap to incorporate now and expensive later. Once you’re confident you’re pointed in the right direction, you can move fast.
  • **Show your working.** Share artefacts from the slow phase: requirements docs, design sketches, pre-mortem outputs. This makes the invisible work visible and builds confidence that you’re progressing, not stalling.
  • **Timebox the slow phase.** Give the slow phase a clear boundary: “We’ll spend two days clarifying requirements before we write any code.” This makes deliberate slowness feel intentional rather than open-ended.
  • **Share what you’re learning.** Send brief updates as you discover things: edge cases you hadn’t considered, assumptions that turned out to be wrong. This turns the slow phase into a visible stream of value.
  • **Demonstrate quick wins.** Build a throwaway prototype or mockup early to show stakeholders you can move fast when needed, buying you credibility for the slower, more deliberate work. ([View Highlight](https://read.readwise.io/read/01km7w605bmspj365yserysn7m))
    - Note: Zależnie od faz i trybu w jakim działasz korzystaj z AI jako generatora lub sparing partnera. Bądź świadom w jakiej fazie jesteś bo z pewnością ktoś będzie kładł na Ciebie presję.
