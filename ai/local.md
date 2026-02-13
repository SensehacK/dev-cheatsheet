
## Intro


### Local knowledge base

Use this software to keep a track of your knowledge base [obsidian](obsidian.md) & then work with localLLM to connect and train it.

[use-local-ai-models-to-privately-chat-with-Obsidian](https://docs.gpt4all.io/gpt4all_desktop/cookbook/use-local-ai-models-to-privately-chat-with-Obsidian.html)

[github | LocalDocs wiki](https://github.com/nomic-ai/gpt4all/wiki/LocalDocs)

### Reddit post

[copy pasta](https://www.reddit.com/r/ObsidianMD/comments/1fhhbnw/comment/lneoge9/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) 
```copy
Wow. I disagree with a lot of the comments here.

I use a local, private LLM (Large Language Model) with my Obsidian notes. GPT4All's LocalDocs and Kotaemon's RAG injest Markdown and PDFs on my PC. ([https://docs.gpt4all.io/gpt4all_desktop/cookbook/use-local-ai-models-to-privately-chat-with-Obsidian.html](https://docs.gpt4all.io/gpt4all_desktop/cookbook/use-local-ai-models-to-privately-chat-with-Obsidian.html)). Here's a couple of my use cases:

* Needle-in-Haystack: some LLMs are good at semantic search. I also have Recoll, a lexical/literal search setup, and OmniSearch plugin but those often find lots of unrelated stuff. And literal searches require a priori knowledge, aka. I must remember the author's name to find my notes about that author. There's LLM benchmarks for needle-in-haystack. ([https://www.anthropic.com/news/claude-2-1-prompting](https://www.anthropic.com/news/claude-2-1-prompting))

* Q&A: some LLMs are good at answering questions from large texts, called DocQA generally. This is related to searching but can be scoped to specific notes/docs. The LLM searches my Notes based on implied intent of the question instead of only literal or a priori knowledge. For example, I can ask the LLM: "which author did I read that advocated for critical thinking skills?" and the LLM can give a list of names from my Notes. There's another set of LLM benchmarks for document Q&A. ([https://chatqa-project.github.io/](https://chatqa-project.github.io/))

* Summarize: LLMs are great at summarization. A lot of my Obsidian notes are annotations from my readings, and I don't always write book reviews/summaries. So the LLM will "jog" my memory about the topic of the Notes when I didn't notate a review/reflection of my own.

* Citations: many LLM setups now include citations back to my Notes. Instead of the LLM doing just generated text as a black box, it links to its sources from my Obsidian Vault. This is probably the most powerful feature that rolled out late last year. GPT4All does citations. (Video of one of its creators that integrated with their Obsidian Vault: [https://www.youtube.com/watch?v=gQcZDXRVJok&t=65s](https://www.youtube.com/watch?v=gQcZDXRVJok&t=65s))

I do not have philosophical chats about my notes. Why bother?? And I've read both advocates and critics of AI. AI is a very poor term. Basically LLMs can be a useful NLP (natural language) tool for certain tasks on large amounts of text and ... Obsidian Vaults are large amounts of text.

Using local tools instead of public chatbots does take skill by the user. One-shot questions don't usually perform well, but Chain of Thought prompts perform very well. (Kotaemon includes a COT prompt framework so the user doesn't have to spend a lot of time typing.) The user also needs to be aware of Instruct trained models, and the tunables for LLMs, like temperature. It does take some effort to make LLMs useful, and a healthy dose of skepticism.

Local, private LLM setups will run on beefier laptops/PCs. Usually 16GB memory minimum, though setups like Kotaemon need more. They're getting better every day and can perform many tasks even if not at GPT4 level.
```

## Reference


[github | gpt4All](https://github.com/nomic-ai/gpt4all)

