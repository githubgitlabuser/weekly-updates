# Week 11 updates

- Instead of the chunking, embedding based approach we decided to move on with a simpler search based approach similar to what Claude Code (CC) does. This will give more control and better iteration.

- This week I tried to improve the CC equivalent direct approach program run better. 

- Realising that EIPs can be cross-client. So searching only inside CL would mean we won't find MANY things and the program will incorrectly conclude that these aren't implemented whereas in reality they are probably implemented in Geth. 

- So I should write a separate program that will take EIP as input and segregate entities based on whether they belong to an EL or CL. Then our program will take that as an input and another input which will specify if our current repo is EL or CL (e.g. Prysm is a CL) and then it will know what to look for. 

- For now it will be simpler to take an EIP that is either CL-only or EL-only and continue working on the core logic.