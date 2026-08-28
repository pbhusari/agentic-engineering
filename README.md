# agentic-engineering

Daily notes on what's on Hacker News, written by a scheduled Claude Code routine.

Each day it pulls the current HN front page via the public Algolia API and drops a short dated write-up into `digests/`, picking out a handful of stories worth a second look and saying why. No filler, no "top stories today are:" bullet dumps.

## Layout

- `digests/YYYY-MM-DD.md` — one file per day.

## Latest Deep Dive

<!-- STUDY:START -->
### 2026-08-28: [Small Models Have Arrived](https://calv.info/small-models-have-arrived) ([HN discussion](https://news.ycombinator.com/item?id=49466917), 578 points, 263 comments)

Calvin French-Owen's post makes a narrow but real claim: a class of small, fast models (he names gpt-5.6-luna and GLM 5.3) has crossed a cost threshold that changes what kind of product you can build with an LLM in the loop. His example is a personal news-digest agent that searches his own name across HN, Reddit, and Twitter, figures out what he'd want to read, and assembles a page — a task that cost roughly a dollar in API calls on a Sonnet-class model and now costs about a dime on luna. That's not a benchmark result, it's a receipt, but it's a useful one: a dollar per run makes a $30/month consumer subscription math out badly, a dime per run doesn't.

There isn't much technically novel here. Cheap, fast, "good enough" models have been getting cheaper on a fairly predictable curve for two years — distillation, quantization, better small-model training recipes, and straightforward price competition between labs have all been pushing this direction, and plenty of infra companies (Groq, Together, Fireworks, the labs' own mini/flash tiers) have been selling exactly this pitch. What French-Owen adds isn't a technical insight, it's a framing borrowed from his Segment co-founder Peter: most knowledge work splits into "IQ 180" work — the rare, hard-to-automate insight that unblocks everything else — and "token spewer" work, the high-volume, low-difficulty grinding (following up, nudging, routing, summarizing) that dominates actual headcount at a company. His claim is that frontier models will keep getting hoarded for the first bucket while cheap models finally become good enough for the second, and that this second market is the one nobody's built consumer products for yet because token costs made it uneconomical.

The weak spot is exactly where the post gets hand-wavy: "the results are pretty decent" is doing a lot of work with zero quantification of how much quality luna is actually giving up relative to a frontier model on the same task, and there's no attempt to characterize which tasks tolerate that gap and which don't. That distinction matters more than the cost number. A cheap model that's 90% as good at drafting a status update is a fine trade; a cheap model that's 90% as good at deciding whether to refund a customer or approve a merge is not, and the post doesn't engage with where that line sits. The closing gesture at "new harnesses, prompt injection safety, roles and permissions" needed to make cheap-model agents safe in a business context is the actual hard research problem being raised here, and it gets a sentence instead of an argument.

That said, the economic argument is worth taking seriously for anyone working on agents rather than chat. Multi-step agentic workflows — parallel tool calls, retries, self-consistency checks, tree search over candidate actions — have mostly stayed benchmark curiosities because running five or ten cheap-but-not-free frontier calls per task doesn't survive contact with a real cost budget. If small-model quality keeps closing the gap on the kind of bounded, well-specified subtasks that dominate agent traces (classify this, extract that, retry this tool call with a fixed schema), then test-time-compute techniques that look expensive today become the default architecture rather than the exception. That's a bigger deal for how agents get built than anything about consumer apps, and it's the part of this post that's actually forward-looking rather than anecdotal.
<!-- STUDY:END -->

## Why this exists

Mostly to keep a daily habit of skimming HN without doing it manually, and to have a searchable log of what caught attention on a given day.
