# Update of week 1 and 2

Weeks 1 and 2 had overlap of work so I decided to combine it into one post. 

During these weeks I was focussing on the following:
- Figuring out the updates and choices of technology for my AI solution
- Crafting them together in a meaningful way so that in theory it looks clear 
- Preparing for the travel to France

## The tech details
- Initially I was thinking in the lines of PRs mostly and relying on the model's knowledge of the codebase as pre-existing. 
- But after some discussions and checks it was clear that the model's codebase knowledge can be too outdated or non reliable. For example most LLMs have limited understanding of Nimbus
- Even fine-tuning may not be very efficient as they take time and resource
- So better to actually use the codebase directly. 
- But in this case the naive way will eat up the context length. 
- So the better approach is to use Agent + Knowledge base served up by MCP servers. 
- We have 3 sources of knowledge base: Codebase, EIP (EIP doc, test specs, EIP ontology), PRs which implement an EIP
- So the idea is to parse these knowledge base by using a vector storage and embedding paradigm so that we can store meaningulf information in vector embeddings.
- Then those embeddings can be exposed via MCP servers. 
- These MCP servers (or function calls) can be used by an Agent. 
- The agent can act in a  think - act - execute - write framework loop. This can be set up in its system prompt which is an important thing to get right.
- For example the agent is asked to think step by step about how EIP might be implemented based on its specs or features and then it finds these individually one at a time. 
- This way it is more focussed and doesn't reach context length limit that easily. 
- Microsoft's Autogen AI Agent is one such example. So this can be a starting point. We can try other AI agents later e.g. CrewAI. 
- Various AI agents have different way of funcitoning so it is worth exploring a bunch of them eventually. 
- So the flow can be the following: git clone the codebase, EIP github, specs/tests etc -> Chunk and store in vector database -> expose MCP server -> Ask the Agent to start its analysis loop -> It does one step at a time -> Eventually writes a report for one particular client -> Compares reports of multiple clients -> Gives its final comparison report. 
- The hope is that it will at least cover the edge cases or divergence of implementation. 
- Best case scenario is for the Agent to find actual bugs. 
- I need to figure out how to teach the system based on the previous bugs so that we at least learn from historical mistakes.
- The above teaching can be through finetuning the AI model with bug history data or a separate file that can act in a RAG way or manually condense key areas of bug and make it part of the system prompt of the AI Agent.
- I started working on the PPT (which continued to the week of EthCC): https://docs.google.com/presentation/d/1LpxBvbz30qVwpplKAX2DC66CfZuEb7kNTB4qlZq_hHA/edit?usp=sharing  

## Non technical work during the weeks
- I prepared for the travel to France: 30 hour journey! 
- It was worth it -> will update the experience in the conference in the week 3 report. 

I thank Mario for his valuable feedback. I haven't been able to talk to Fredrik much but will be in touch with him soon.
