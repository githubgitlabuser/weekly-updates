# Update of week 10

## Call with Fredrik

- I shared my progress and a newer future plan i.e. to use Reinforcement Learning to train the system of the past security vulnerabilities. So that it learns to look for similar cases. If successfully implemented then this can make the client code more robust and we will at least make sure we don't repeat our mistakes from the past.

- I got the following example case which can be a good case study to test:
    - The bug scenario: https://github.com/ethereum/execution-spec-tests/pull/1993
    - The fix from reth: https://github.com/bluealloy/revm/pull/2872
    - The fix from besu: https://github.com/hyperledger/besu/pull/9054
    - The idea is that if I take the commit from before this PR then they obviously have the bug. So ideally my system, once built, should be able to find the bug. I might try in stages: 
        - Simply ask details about this scenario regarding if it is implemented correctly (this should be testable with what I have now)
        - Ask for the general EIP implementation and hopefully this bug will emerge as a finding (this can only be tested once I have fully built the solution)

Two future todo items:
 - Research on Claude Code reverse engineering
 - Getting Autogen to Autonomously work

## Non-naive Chunking and Embedding 

- Currently my approach has been the naive chunking and embedding which is a start but not ideal for codebases.
- I got to know that there are code specific embedding models (CodeBERT, GraphCodeBERT, UniXcoder) so that should be used. Rather than text specifc ones like text-embedding-ada-002. 
- Doing AST and THEN RAG is better. 
    - Each function becomes a chunk.
    - Hierarchical chunking e.g. level 1: functions, level 2: files 
    - Add metadata to a chunk e.g. filepath, parent, line numbers etc. Otherwise they will lose context. Metadata will be useful in both filtering during retrieval and providing context to the LLM in the final prompt.