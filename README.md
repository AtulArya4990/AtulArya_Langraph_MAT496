# Langgraph by Atul Kumar Arya

MODULE 1 (Introduction):

 Lesson 1 (Motivation):
     I learned that using just one AI model is limited because it can not use tools or do complex tasks on its own. So, we use something called LangGraph to build a           step-by-step plan for the AI.
     The tricky part is that the more freedom and control you give to the AI, the more likely it is to make mistakes. LangGraph is cool because it lets me decide            which steps in the plan are fixed and which steps the AI can control. This way, I can give the AI some freedom but still keep the whole system reliable and            under my control.

 Lesson 2 (Langsmith studio):
     State schema serves as a input schema for all nodes and edges, here we used TypeDict as our schema. Edges connects nodes. After defining the edges and nodes in         the form of code which acts as a graph we  contructed  a simple langgraph. We used "Start" and "End" node to point the start and the terminal point of the graph.
     This was the output graph:
       <img width="292" height="423" alt="image" src="https://github.com/user-attachments/assets/dc9acb6a-bae0-4b39-aaa9-34e2f0ce347e" />
     In graph invocation, compiled graph implements the runnable protocol, invoke is used to call the function(graph), here 50% rule is applied if the number of sub         edges are two and sometimes it will print happy and other times sad.
       <img width="568" height="207" alt="image" src="https://github.com/user-attachments/assets/36f7b701-f838-4690-bd64-640f768571a8" />
       .
     Tweaking-: In this section i made an example with using the basic garph and i made total 5 nodes in which 1 was the main node and the other 4 nodes were the sub        -edges.
       <img width="491" height="441" alt="image" src="https://github.com/user-attachments/assets/95b82bf9-68a9-4add-81f8-98107cc07e1b" />
     I also invoked the graph and asked about my favourite color so it had 3 options and while running the code again and again it was giving the different answer.
       <img width="846" height="219" alt="image" src="https://github.com/user-attachments/assets/0948a437-c7a2-4ad0-a1b3-e24673a8eddc" />


      
