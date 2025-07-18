# Update of week 4

In week 4 I started writing the project proposal and also being a bit hands-on on the components such as indexing and MCP server. 

I also messaged Fredrik with the slides and the video of my talk from Cannes. He mentioned he will go over it and will get back to me regarding this. 

## Indexing

- I got a general idea about how to use pgvector with postgres. 
- Wrote an example code for encoding and chunking and saved in the postgres+pgvector which seemed to work fine. 
- The naive indexing/chunking mechanism isn't ideal but will form a starting point of the project. 
- For cases where there is lot of text (like in our case), it is worth checking other approaches like graph based approach. 

## MCP server

- Did some research on what are the typical pattens in which custom MCP servers are written. 
- Researched how to actully call and test existing MCP servers. 
- Ran couple of custom MCP servers and did some testing on them. 