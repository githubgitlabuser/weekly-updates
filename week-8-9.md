# Update of week 8 & 9

These are the following work that were done during week 8 and 9:

## Fulu Specs Visualizer

- I created a visualizer for fulu specs: https://githubgitlabuser.github.io/specs-knowledge-graph/fulu_real_knowledge_graph.html 

- This involved text chunking, extracting entities and relationships from the fulu documentation, creation of knowledge graph and showing it using a web interface. Pyvis package was used to do the visualization. I used LM Studio for LLM (Qwen/Qwen3-Coder-30B model) and nomic-embed-text:latest for embedding model which was running using ollama. 

- I then read the fulu specs using this visualizer as an option aid and it was very useful. Especially the part that you can search for any entity (function, constant, variable etc) and get to its node directly. Then you can see which other entities it directly interacts with and HOW it interacts. e.g. get_data_column_sidecars USES DataColumnSidecar. Or compute_fork_digest RETURNS ForkDigest. I feel this could be improved a bit by using a better LLM model.

## Research on how Claude Code works

- When Fredrik and I discussed we had agreed on moving forward with two paths: 
    - 1. The project proposal that I have written. 
    - 2. Trying to replicate the way Claude Code or Cline work. Because they are known to work reasonably well for large codebases especially Claude Code.

- But Claude Code isn't open source.

- I found some material from a person which claimed to have reversed engineered it and he mentioned from key insights:
    - The System Prompt of Claude Code is extremely vital.
    - If you want your agent to certainly do something, you have to keep reminding it basically every time. For example, Claude Code almost always keeps track of a todo list. It is not hardcoded but rather consistent prompt engineering! Something I wouldn't have expected. 
    - The architecture roughly is: client - LLM - Tools. With the addition of system prompt on every session. So the client likely goes back and forth between LLM and tools. 

- What is not clear to me: 
    - How Claude Code is so good at fetching the relevant file or function. Because just normal text search can give hundreds of relevant files which are relevant to a particular entity. But it quickly filters out. In my project proposal which is embedding based, at least there is something like cosine similarity search which can help give relevant stuff but Claude Code clearly doesn't do embedding. 
    - How it continues doing long tasks without going off track. I sort of know it is a lot to do with having a really good LLM but that it still limited by context length. 
    - How exactly the auto compaction works? Is it better to let it auto compact or simply stop and create a new session? I have used Claude Code for some time but still not sure which one is better here. 

## Wroking on an autonomous demo program using Autogen Agent

- A key component of the solution I am building is having an agent 'brain' that can autonomously keep executing tasks on its own until it is satisfied with the answer. I am currently still in the process of getting a small program to work. It is fairly clear that it doesn't support it out of the box so I will need to combine good system prompt with tooling support. 


## TODO for week 10:

- Finish the Autonomous Autogen demo that can run multiple steps on its own.
- Reverse engineer Claude Code: So far I have only heard from other's opinion, this week I will try to actually do the reverse engineering hands on to get more decisive answers. 
- Meeting and discussion with Fredrik