# Meta Muse Can Run Your Errands. One Seller Found Out It Can Also Share Your Address.

## 5 headline options

1. **Meta Muse Can Run Your Errands. One Seller Found Out It Can Also Share Your Address.**
2. Meta Muse Explained: What the AI Agent Does, How It Works, and What Real Users Found
3. I Read Every Meta Muse Story I Could Find. Here's Who Should Use It, and How.
4. The AI Agent That Keeps Working After You Close the App. Should You Trust It?
5. Meta Muse Is Managing People's Lives. Here Are the 3 Questions I Ask Before Trusting It.

**Chosen headline:** Meta Muse Can Run Your Errands. One Seller Found Out It Can Also Share Your Address.
**Subtitle:** Meta launched Muse on 8 September 2026. Here's what it does, how it works under the hood, three stories from real users, and the setup I'd use before giving it access to anything that matters.

![Meta Muse thumbnail: It shared his address](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/01-hero.jpg)

▶ **Watch the full video on YouTube:** Meta Muse Is Managing People's Lives… But Something Went Wrong [LINK — to be added]
▶ **Watch the short version (Instagram reel):** [LINK — to be added]

---

## TL;DR

- **Meta Muse is an AI agent, not a chatbot.** You give it a goal, and it plans the steps and does the work: it opens websites, fills forms, books things, and keeps working after you close the app.
- **It runs on its own computer in the cloud.** Meta calls it Muse Secure VM, a virtual machine with its own browser and workspace. A separate guard called **Sentinel** has to approve anything it sends to the internet.
- **It asks before sensitive actions,** like sending an email or making a purchase, and it keeps an audit trail of what it did.
- **Real users are impressed and a little scared.** One Reddit user says it books restaurants and haircuts and sets its own follow-up reminders. An AP report describes a seller whose Muse accepted an offer and shared his home address with a buyer, without his knowledge. Meta traced it to an "always allow" permission he'd granted earlier.
- **My rule: start with low-risk tasks, read every permission, and ask three questions before you connect anything.** The step-by-step setup is below.

---

## My life needs an assistant

Who decided that being an adult means managing about 500 things every single day?

I have a full-time job, a toddler, meetings, groceries, appointments and emails. And somehow I'm also supposed to remember when the toothpaste is running out. Some days I genuinely wish I could hire another version of myself.

So when Meta announced an AI agent that can book, plan, shop and even negotiate a bill for you, I paid attention. Then I started reading what actual users were saying. One reviewer called it helpful and scary at the same time. One person's agent set itself a reminder to follow up on a booking. And one person's agent shared his home address with a stranger during a sale.

This article covers what Meta Muse actually does, how it works, what real people are experiencing, and whether I'd trust it with my life. I work with AI every day, and I build AI products, so I'll also share the questions I ask before I let any agent touch my accounts.

---

## What is Meta Muse?

Meta introduced Muse on **8 September 2026** and calls it "a secure, private personal AI agent". In Meta's own words: *"It doesn't just answer questions, it actually does the work."*

The simplest way I can explain it is this. Think of ChatGPT as someone you can ask for help. They give you advice, a list, a plan, and then you still have to go and do it yourself.

Now imagine giving that assistant access to tools: a browser, your email, your calendar, a checkout. Now it can go and complete the task. That's the idea behind Muse.

![A chatbot answers. An agent gets tools.](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/02-chatgpt-vs-agent.jpg)
*A chatbot answers you. An agent gets tools and acts. Still from my YouTube video.*

You don't need to explain every step. You tell it what you want to achieve, and it works out how to approach the task. Meta describes it like this: once a person shares a goal, Muse *"helps them develop a personalized plan and coordinate their time and resources, then advances the work on its own."*

### A concrete example

Instead of asking, *"How should I organize my son's birthday party?"*, I could say:

> Help me plan a dinosaur-themed birthday party for 30 people. Find decoration options, create a shopping list, and organize everything by budget.

![The goal-style prompt for a dinosaur-themed birthday party](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/03-goal-prompt.jpg)
*My example of a goal-style prompt, not a Meta demo.*

Muse could then research the options, help build the plan and work through supported tasks using the services you've connected. Meta's own examples are similar: suggesting a menu for a dinner party, remembering friends' dietary restrictions before sending invites, turning a recipe reel you saved on Instagram into a grocery list, booking travel, and *"selling a car for more, lowering a bill"*.

Now that sounds useful. I have one condition, though: please don't order 200 dinosaur balloons without asking me first.

---

## How Muse actually works

Engineering hat on. I promise this won't turn into a computer-science lecture, but three pieces matter if you want to understand the risks.

### 1. Its own computer: Muse Secure VM

Muse launched on an AI model Meta calls **Muse Spark**. (Meta said on 12 October that newer "Muse Wonder" models will soon power Muse too, rolling out first to subscribers.)

The bigger idea is where Muse works. Meta built something called **Muse Secure VM**. VM stands for virtual machine. Meta's launch post says: *"Muse runs on Muse Secure VM, a dedicated, virtual machine (VM) that houses both the agent and a person's data."*

![Meta's description of Muse Secure VM](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/04-secure-vm.jpg)
*Source: Meta Newsroom, 8 Sept 2026.*

Imagine giving your AI assistant its own computer, its own browser and its own workspace. Meta's safety team puts it this way: *"You and your Muse share your own dedicated computer in the cloud… Each Virtual Machine(VM) is an isolated linux box with a browser and enough storage, CPU, and memory to do real work."*

![Your own dedicated computer in the cloud](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/05-own-computer.jpg)
*Source: Meta AI Research, "How We Built Safety Into Muse", 8 Sept 2026.*

So when you ask Muse to research a holiday, it can open websites, look through options and work across several steps. It can also connect to supported apps, including your email and calendar.

### 2. A guard at the door: Sentinel

This is the part I find most interesting as an engineer. Meta built a separate protective system called **Sentinel** that checks actions before they reach the internet:

> "A separate Sentinel agent runs on that same machine, kept apart from Muse at the system level. Nothing Muse does reaches the internet unless the Sentinel approves it, and it asks the person for permission when needed."

![Nothing reaches the internet unless Sentinel approves](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/06-sentinel.jpg)
*How the pieces fit: Muse works inside its own computer. Sentinel stands between it and the internet.*

Think of it as a security guard supervising your AI assistant. The safety post is even blunter: *"Muse proposes actions, but only Sentinel can grant permission to perform action."*

![Muse proposes. Sentinel decides.](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/07-sentinel-decides.jpg)
*Source: Meta AI Research.*

### 3. Approvals and an audit trail

For sensitive actions, Muse is designed to ask you first. Meta says *"Muse checks with the person before sensitive actions like sending an email or making a purchase."* You can also review what it did: Meta promises *"a complete audit trail of everything it has done and plans to do"*, and you can watch it work in the browser and take over at any time.

**But this is important: permission settings matter a lot.** Giving your AI permission to act is not the same as giving it good judgment. Meta's own safety post says it plainly: *"Muse can and will still make mistakes."* We'll come back to that, because the most uncomfortable story below comes down to a single setting.

---

## What real people are experiencing

Muse has been out for about six weeks. I went through reviews and people's experiences online, and the results are a mixture of impressive, useful and slightly terrifying.

### Story 1: "Helpful and scary at the same time"

A Wall Street Journal personal-tech columnist, Nicole Nguyen, tried Muse and published her review on 28 September under a headline that sums up most of what I read: *"I Tried Meta's Muse AI Agent. It's Helpful and Scary at the Same Time."* The subhead names the trade-off: *"The more data you hand over, the more this talented personal assistant can do for you."*

That's the core tension of every personal agent. The more it knows, the more useful it becomes, and the more it can get wrong. (The full review sits behind WSJ's paywall, so I'm only quoting what's public.)

### Story 2: The AI that follows up

On 12 October, a Reddit user posted in r/AI_Agents after two weeks with Muse: *"I asked it to book me restaurants, movie tickets, haircut appointments, etc."*

What impressed them was this:

> "booking is not open yet, so it just sets a reminder for itself to followup at a later time"

![A Reddit user's account of Muse setting itself a reminder](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/08-reddit-reminder.jpg)
*Source: Reddit, r/AI_Agents, 12 Oct 2026 (self-reported).*

Now that is interesting. We're moving beyond an AI that only responds when you ask a question, towards one that can remember an unfinished goal and come back to it later. Of course, this is one person's account, not a controlled test.

### Story 3: The Marketplace address

This one genuinely made me uncomfortable.

According to an Associated Press report from 19 October, Matt Robb, a Toronto-based content creator, wanted to sell his computer keyboard on Facebook Marketplace. As an experiment, he put Muse in charge of the listing. Muse struck a deal on its own and shared his home address after agreeing to a pickup, all without his knowledge. He had assumed the agent would check with him before sharing that information or accepting offers.

![The AP report on Muse accepting an offer and sharing a home address](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/09-ap-report.jpg)
*Source: Associated Press, 19 Oct 2026, via The Washington Times.*

Imagine asking AI to sell your keyboard, and suddenly it's telling a stranger where you live. No, thank you!

Here's the part that matters most. Meta told him the address sharing came down to **"always allow" permissions** he had granted when he first gave Muse access to his Marketplace profile, where his pickup address was part of a broader template. Meta also acknowledged a separate pricing error, in which Muse seemed ready to accept less than his minimum price.

If Meta's explanation is right, Muse did what it was technically permitted to do, and that wasn't what he intended.

---

## Can you trust it? The 3 questions I always ask

**The more useful an AI agent becomes, the more information it may need.** Your emails, your calendar, your shopping preferences, maybe your contacts.

As someone who builds AI products, I ask three questions before I trust any agent, Muse included:

1. **What can this agent access?** Every connected app is a door. Count the doors.
2. **What can it do without asking me?** This is the question the Marketplace story is about. "Always allow" is a decision you're making ahead of time, for every future situation you can't see yet.
3. **Can I see exactly what it has done?** If I can't audit it, I can't trust it.

![What can it do without asking me?](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/10-three-questions.jpg)
*Question 2, with the AP paragraph about "always allow" permissions.*

To be fair to Meta, its launch post covers a lot of this:

- **Credentials:** *"Muse has no visibility into people's passwords or payment methods. Any credentials a person shares with Muse go into secure storage, so Muse can use them without seeing them."*
- **Connected apps:** *"People choose which apps Muse connects to and exactly how much access it gets."* You can change access or disconnect a service at any time.
- **Activity:** the audit trail I mentioned above.
- **Ads:** Meta says *"Muse doesn't share a person's conversations or the data in their VM with Meta's ad systems."* Its own safety post adds a nuance worth knowing: what Muse does for you on the web, like a reservation or a product it finds, can still influence the ads you see.

But that doesn't mean every privacy concern magically disappears.

---

## How to try Meta Muse safely: step by step

If you want to explore it yourself, here's the process I'd follow.

1. **Check availability.** Meta says Muse *"is rolling out in the US on iOS, Android, and muse.ai"*. If you're outside the US, availability may vary.
2. **Get the official app only.** Go to muse.ai or the official Muse app in your app store. Don't install lookalike "Muse AI" apps.
3. **Know the pricing model.** Meta says it's *"free for most of what people need, with subscription plans for people who want to do more."* Check the current plans in the app before you rely on it.
4. **Start with one low-risk task and no connections.** For example:

   > Help me plan five easy family dinners for next week. Create a grocery list and group everything by category.

5. **Read the plan before it acts.** A good agent shows you its steps. If a step surprises you, stop and ask why.
6. **Connect one service at a time.** When you connect email, Meta says you choose *"whether it reads their mail or can also send on their behalf."* Start with read-only.
7. **Never tick "always allow" on anything involving money, your address, or messages to other people.** Keep approval on for purchases, emails and anything public.
8. **Review the activity history after each task** for the first week. You're learning how it behaves, the same way you'd watch a new assistant's first few days.
9. **Widen access only when it's earned.** If it has done ten low-risk tasks well, give it the next level. Not before.

![Start with low-risk tasks](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/11-low-risk.jpg)
*Research a holiday, organize an event, make a grocery list. That's where I'd start.*

### My low-risk vs review-every-step checklist

**Fine to start with:**
- Researching a holiday or comparing options
- Organizing an event or a family schedule
- Making a grocery list from a saved recipe
- Drafting (not sending) an email

**Review every step:**
- Anything that spends money
- Sensitive emails, or any message sent in your name
- Sharing personal information: your address, phone number, documents
- Anything on a marketplace, where a stranger is on the other side

And please don't connect your entire digital life just because an AI has a pretty interface.

![My recommendation: start small](https://guljabeen.github.io/TWG-AgentKit/articles/meta-muse/images/12-start-small.jpg)
*My recommendation, in one line: start small.*

---

## Common mistakes and quick answers

- **"It asks before sensitive actions, so I'm safe."** Only if you haven't told it not to ask. "Always allow" switches off the very check you're relying on.
- **Connecting everything on day one.** Every connection widens what can go wrong. Add one at a time.
- **Skipping the plan.** Agents fail quietly: the wrong item, the wrong date, a price below your minimum. Read the plan and the activity log.
- **Expecting every website to cooperate.** Sometimes they won't. Amazon, for example, blocked Muse from shopping on amazon.com from 20 September, calling it an unauthorized AI agent under its Conditions of Use. Agents depend on sites letting them in.
- **Is Muse retraining on my data?** Meta's privacy claims are about ads and credentials. Read the in-app privacy settings for your own account before you connect anything personal.
- **Is it available outside the US?** Meta's launch post says it's rolling out in the US.

---

## My take

You know what excites me most about Muse? A grocery list isn't new. We've had tools that do that for years.

What's new is AI that understands a goal, plans the steps, uses tools and follows through. That's a much bigger shift.

But here's where I think we need to be realistic. We're not at the point where you can hand your entire life to an AI and forget about it. Sometimes it will make mistakes. Sometimes websites won't cooperate. And sometimes it might do what you technically permitted, but not what you actually intended.

So for me, the future of agents is about reducing the repetitive work humans have to do, while the judgment stays with us. If AI can give me even one extra hour to spend with my family, go to the gym, or simply enjoy my coffee while it's still hot, I'm interested.

Now I want to know what you think. Would you trust an AI agent with your personal life? And if you had Muse today, what's the first task you'd give it? Mine would be organizing all those saved Instagram recipes I never actually cook.

---

If you want **five practical tasks you can try with personal AI agents, including prompts you can copy**, comment **MUSE** on the reel or the YouTube video and I'll send them to you.

I'm Gul — Director of Engineering at Hyly and founder of Tech With Gul, working with AI every day and making it easier for everyone to understand and use. If this was useful, follow me here, on YouTube at [@techwithgul.ai-00](https://www.youtube.com/@techwithgul.ai-00) and on Instagram at [@techwithgul.ai](https://www.instagram.com/techwithgul.ai/).

---

## References

Primary sources:

- Meta Newsroom, "Introducing Muse: The World's First Personal AI Agent Built for Everyone" (8 Sept 2026; Secure VM, Sentinel, approvals, audit trail, credentials, connected apps, ads, rollout, pricing model): https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/
- Meta AI Research, "How We Built Safety Into Muse" (Tarek Sheasha, 8 Sept 2026; dedicated computer in the cloud, Sentinel as the sole permission authority, "Muse can and will still make mistakes", ads nuance): https://research.meta.ai/blog/security-and-safety-for-ai-agents-our-approach-with-muse
- Meta Newsroom, "Introducing Muse Wonder" (12 Oct 2026): https://about.fb.com/news/2026/10/introducing-muse-wonder-models/

User stories:

- The Wall Street Journal, Nicole Nguyen, "I Tried Meta's Muse AI Agent. It's Helpful and Scary at the Same Time." (28 Sept 2026; headline and subhead only): https://www.wsj.com/tech/personal-tech/meta-muse-ai-agent-review-ab956101
- Reddit, r/AI_Agents, "Two weeks into using Meta Muse I'm asking - how is this not AGI?" (12 Oct 2026, self-reported): https://www.reddit.com/r/AI_Agents/comments/1x44kpr/two_weeks_into_using_meta_muse_im_asking_how_is/
- Associated Press, Wyatte Grantham-Philips (19 Oct 2026), as syndicated by The Washington Times: https://www.washingtontimes.com/news/2026/oct/19/artificial-intelligence-good-personal-information-share-raises/

Further reading:

- GeekWire on Amazon blocking Muse (Sept 2026): https://www.geekwire.com/2026/amazon-blocks-metas-muse-ai-assistant-in-new-standoff-over-agentic-shopping/

> Images: stills from my YouTube video. Meta, AP and Reddit text in the images are crops of the original pages, credited on each image. The birthday-party prompt and the Marketplace chat in the thumbnail are my own illustrations.

---

**Tags:** Artificial Intelligence · AI Agents · Meta · Privacy · Productivity · Technology · Tech With Gul
