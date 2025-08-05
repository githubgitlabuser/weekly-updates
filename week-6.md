# Week 6 update

Week 6 was mostly about the agent research and corresponding running of code to see if I understand how to make it to work. This is the last stage remaining before I can start working on the full solution. 

# Autogen Agent & graphrag Research

Some important relevant features:

- It has a group chat feature of agents. So you can define multiple specialised agents and they do their own part. This is the relevant sub package: RoundRobinGroupChat. Seems like it may need an orchestrator agent which can pick and choose between the list of specialised agents. 

- Some mcp server integration example: https://microsoft.github.io/autogen/stable//user-guide/agentchat-user-guide/tutorial/agents.html#model-context-protocol-mcp-workbench 
But I need more concrete example with multiple mcp servers that are configurable the way I want. 

- Tried graphrag (https://microsoft.github.io/graphrag/get_started/). After many iterations, finally managed to get it to run with local models. 
It needs an inference model and an embedding model. The inference model can be sort of free through groq api. But they don't provide embedding endpoint. So it looked like I will really need to pay for OpenAI api credits as OpenAI provides embedding model. But I searched and realised LM studio can also support embedding model. But LM studio can only run either an inference model or embedding model. Not both. So I installed ollama and used ollama to run embedding model and LM studio to run inferencing model. Then I ran the graphrag getting started example and it seemed to somehow work but partially as the local model was too slow for it. Also the indexing itself is really slow. So I will need to think of a way to make it faster or somehow get free OpenAI api credits or simply take the tough road and let it run for hours to truly see how long a somewhat small repo takes to index. This is currently a work in progress. 

- Once the graphrag is all set, then I can run the Autogen with it to have a decent working example. After that I will be in a position to move forward and build the full software solution. 
