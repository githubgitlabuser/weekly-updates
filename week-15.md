# Week 14 & 15

In week 14 and 15 I worked on improving the two track search approach in the following ways:

- I created a separate program for creating callgraphs. This is Golang focused for now. But later to be done for othr languages. 

    - The idea is that when the program doesn't find enough evidence for a feature to have been implemented properly, it could use call graph to concretely know the nearby entities of a feature. For example a function can know which other functions it calls or vice-versa so that we have a more holistic view of the implementation. This will give the judging LLM a better view and more context to make a judgement on it. 

- I also created a separate sub program that does per feature searches using LLM separately. So this function takes one feature and up to 6 (configurable) code evidences where this feature appears and then asks the LLM to give a verdict. This verdict then gets added to "Evidences" in order to finally compile all approach results together to produce a final report. 
    - A key addition I made is the "description" field to the feature/requirement which was missing before. So a feature/reqirement now has both concrete as well as LLM derive fields so that it is a complete set in itself. 
    - A requirement has the following fields now:
        - id
        - kind (("func" | "field" | "constant" | "rpc_method" | "type" | "integration" ))
        - name
        - aliases (e.g. `verify_data_column_sidecar` can also be `verifyDataColumnSidecar`) 
        - description 
        - depends_on (new, not used a lot now but planning to make good use of it)

- Example output of my program so far (just for one feature): 

    ```
    Parsing EIP requirements[CONTINUED]
  🤖 LLM-assisted requirements extraction[CONTINUED]
     ✓ Merged 15 LLM-detected requirements
    ✓ Found 45 requirements:
    • constant: 23 items
      - ALTAIR_FORK_EPOCH, ALTAIR_FORK_VERSION, ATTESTATION_SUBNET_COUNT [CONTINUED] and 20 more
    • func: 10 items
      - compute_fork_version, compute_subnet_for_data_column_sidecar, get_generalized_index [CONTINUED] and 7 more
    • type: 1 items
      - DataColumnsByRootIdentifier
    • rpc_method: 5 items
      - BlobSidecarsByRange v1, BlobSidecarsByRoot v1, DataColumnSidecarsByRange v1 [CONTINUED] and 2 more
    • integration: 6 items
      - fork, on_activation, on_finalization [CONTINUED] and 3 more

    Sample requirement descriptions:
  • verify_data_column_sidecar (func): Verifies if the data column sidecar is valid, checking index range, non-empty commitments, and match

  feature: verify_data_column_sidecar
    code that implements the feature: ./prysm/beacon-chain/blockchain/receive_data_column.go:18

  🔎 Per-feature LLM verdicts

  - verify_data_column_sidecar (func): Implemented — used [0, 2, 3, 4]
  description: Verifies if the data column sidecar is valid, checking index range, non-empty commitments, and matching lengths
  reason: The feature 'verify_data_column_sidecar' is correctly implemented as evidenced by the existence of a function named 'VerifyDataColumnSidecar' in the p2p_interface.go file [idx 4], which is explicitly defined to verify the validity of data column sidecars according to the consensus specs. The function signature and its purpose align with the feature description, checking validity of data column sidecars. Additionally, the function is called in the ReceiveDataColumn method in receive_data_column.go [idx 0], indicating integration into the data processing flow. The evidence shows that this function is part of the core PeerDAS implementation and is used to validate data column sidecars before storage.
  code snippets:
    [evidence 4]:
      func VerifyDataColumnSidecar(sidecar blocks.RODataColumn) error {
    [evidence 0]:
      func (s *Service) ReceiveDataColumn(dataColumnSidecar blocks.VerifiedRODataColumn) error {

    ============================================================
    📊 IMPLEMENTATION STATUS REPORT
    ============================================================

    🎯 Status: **Fully Implemented**       

    📋 Core Requirements Coverage: 95%

      ✅ verify_data_column_sidecar (func): 
     - callsite in ./prysm/beacon-chain/verification/data_column.go:0
       Integration callers -> ['VerifyDataColumnSidecar']
     - definition in ./prysm/beacon-chain/blockchain/receive_data_column.go:18
       func (s *Service) ReceiveDataColumn(dataColumnSidecar blocks.VerifiedRODataColumn) error {
    ```    


- Testings: 
    - I had some interesting insights while testing with Prysm, Lighthouse and Nimbus:
        - Prysm doesn't necessarily adhere to creating all functions or entities exactly as described in the specs. Sometimes the functionality is there but under a different function. My program isn't able to capture it just yet but hopefully in the future. 
        - Both Nimbus and Lighthouse seems to be adhering a bit more to the specs when it comes to having entities with similar names. 
        - The issue sometimes is with camelCase and snake_case. A spec could be defined in snake_case but during implementation the name might be in camelCase. My parsing step takes this into account but not the opposite scenario. That is a todo. 
        - Apparently nim doesn't differentiate between camelCase and snake_case and you can make both work even if you define only one of them! 

- The above have been directly related to my project. But during this time I thought more on how CC does such a good job especially when it comes to iteratively doing things. So I did some more research and thinking on it and came up with an idea of creating a short program to mimic its behaviour. So basically it is an infinite loop having certain stopping condition. There are 3 main elements: the agentic program, an LLM and a set of tools. The program takes the user input, combines with system prompt and feeds to LLM along with a list of available tools. The LLM gives a response which may contain tools. If it does then the agentic program executes that tool, feeds in the result into the response then gives it back to the LLM. It continues until the LLM gives a pre-defined stop condition. All of these constitute one iteration. Then the user is allowed to give his input again and the cycle contiunes. The program I wrote roughly tries to mimic this approach. I could potentially get it to some level where it could be integrated with my differential llming project but for now planning to keep it separate until it shows good promise. 
