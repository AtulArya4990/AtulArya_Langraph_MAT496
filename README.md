# Langgraph by Atul Kumar Arya

MODULE 1 (Introduction):

 Lesson 1 (Motivation):
     I learned that using just one AI model is limited because it can not use tools or do complex tasks on its own. So, we use something called LangGraph to build a           step-by-step plan for the AI.
     The tricky part is that the more freedom and control you give to the AI, the more likely it is to make mistakes. LangGraph is cool because it lets me decide            which steps in the plan are fixed and which steps the AI can control. This way, I can give the AI some freedom but still keep the whole system reliable and            under my control.

 Lesson 2 (Simple Graph):
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

Lesson 3(Langsmith studio) : LangSmith Studio is like a visual dashbord where you can see your ai program working. When you run your program, it creates a             "thread" that shows you the complete history of what happened step-by-step. You can click on each step to see exactly what the ai did, which makes it super          easy to find and fix problems. It's a really helpful tool to understand and track how your ai application is running.

   Tweaking: I gave the input and using the sub nodes it gave the output of sad or happy as i set it to the 50% chances.
       <img width="1899" height="893" alt="image" src="https://github.com/user-attachments/assets/0a4ae8dd-f191-4b07-81b8-53359b9e2501" />


Lesson 4(Chain):A chain is like a fixed recipe where I combine different AI tools in a specific order. First, I use chat messages to talk with the AI, then I            connect it with special tools like calculators or api keys that the AI can use. When I bid these tools to the AI, it learns how to call them automatically.            Finally, I put everything together in LangGraph to create a workflow where the AI can use these tools to answer my questions step by step.
     <img width="1203" height="508" alt="image" src="https://github.com/user-attachments/assets/b5fce36b-1e1e-49a2-bcef-31d72e915688" />

  Tweakings: After the tool calling section, I created a MessagesState class to handle the conversation flow in the graph. I built a simple linear graph with just      one tool-calling node connected between START and END. For testing, I first asked "name the richest sport?" which the AI answered directly without using tools,     identifying American football (NFL) as the richest sport. Then I tested with "Multiply the squares of 20,23 and 20" which successfully triggered the                multiply_squares tool call. The graph handled both scenarios correctly - answering regular questions directly and invoking tools when mathematical calculations     were needed.
     <img width="1052" height="329" alt="image" src="https://github.com/user-attachments/assets/11f868dc-c7f5-40f1-a4cf-5083d59acfed" />
     <img width="1450" height="345" alt="image" src="https://github.com/user-attachments/assets/7ca09a2d-54b5-43f8-abe9-93a534307a4c" />
     <img width="1434" height="511" alt="image" src="https://github.com/user-attachments/assets/6f446362-cd31-4bcd-aac8-794d927b37e5" />
     <img width="1442" height="738" alt="image" src="https://github.com/user-attachments/assets/a13646a7-c5ac-4fbc-9f5c-89302f796c43" />


 Lesson 5(Router): A router is like a smart traffic signal for ai which decides which path to take. When I ask a question, the router checks if it needs to use              special tools or can answer directly. If my question needs calculations or specific tools, it routes to the tool path. If it's a general question, it               answers directly without using any tools. This helps the ai be more efficient by only using tools when really necessary.   
           <img width="200" height="420" alt="image" src="https://github.com/user-attachments/assets/4f0b978f-6ac7-48e6-a56f-a1af7e944130" />
       Tweaking: In this lesson i designed my own divide function:
                    <img width="1006" height="547" alt="image" src="https://github.com/user-attachments/assets/3069ff3a-be52-4e58-96ad-84c9a785d292" />
                 i was successfull in making this work after hours of work and my divide function was ready:
                    <img width="976" height="511" alt="image" src="https://github.com/user-attachments/assets/826c1db5-b366-44ab-8754-0392f2ff2aaa" />
                 I successfully tested the router graph with this new tool and was able to run it on localhost. The router correctly identified when to use the                       divide tool for math questions and when to answer directly for general questions, showing the graph working properly in the studio interface. 
                    <img width="1902" height="905" alt="image" src="https://github.com/user-attachments/assets/815c8734-e7b4-4a11-869c-0d6ed077c758" />


  Lesson 6(Agent): An agent is like a smart asistant that can think and act step by step. It follows a pattern called ReAct where it first thinks about what to                        do, then uses tools to take action, and finally looks at a results to decide what to do next. Unlike a simple router that makes one decision,                       an agent can keep using tools multiple times until it finds the right solution. It keps going back and forth betwen thinking and acting until                       the problem is completely solved. This makes it much smrter and more capable than basic AI systems. 
                    <img width="1385" height="642" alt="image" src="https://github.com/user-attachments/assets/c85a5801-7c18-40d8-b77a-bee6cc571ad3" />
         Tweaking: I created three new square functions (square0, square1, and square2) that each add different numbers to the sum of squares. Instead of using                        cube functions, I built these custom tools and bound them to the agent. When I tested with "squared 4.5 is", the agent successfully used one of                     my square functions and returned the calculated result, showing the agent properly selecting and executing from multiple available tools.
                     <img width="846" height="752" alt="image" src="https://github.com/user-attachments/assets/46fa6ef0-e527-4de4-a115-970a4b56a145" />
                     <img width="1030" height="746" alt="image" src="https://github.com/user-attachments/assets/1a033acc-8fcb-4f6a-b588-8e743d6ac48e" />
                     <img width="1897" height="935" alt="image" src="https://github.com/user-attachments/assets/2602029b-0252-4a0c-aac5-9b50d402e241" />







               

        







      
