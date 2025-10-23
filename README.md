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



   Lesson 7(Agent and Memory): An agent with memory is like a smart friend who acn remember our past conversation. It can look back at what we talked about earlier                                  and use that information to answer new questions better. This memory helps the agent understand context and have deeper, more                                       connected convesations. Instead of starting fresh each time, it builds on our previous chats to give more helpful and acurate                                       responses, just like a real conversation with someone who pays attention. 
                                 <img width="1425" height="416" alt="image" src="https://github.com/user-attachments/assets/ec679387-9bfd-4eee-b2d0-b87fccdca52c" />
          Tweaking: Here using the multiplications, additions and divisions i used to create some example on these operations, I gave it a very tricky question                         using these operations and the agent successfully solved it without using any tools, showing it can handle calculations on its own. It                              demonstrated clear reasoning by breaking down the problem step by step before providing the final answer. The memory system properly tracked                        the entire conversation in the thread with accurate timestamps.
                      <img width="1900" height="935" alt="image" src="https://github.com/user-attachments/assets/af171490-2014-46dc-9ea8-12f18b6c4c36" />
                      <img width="1905" height="875" alt="image" src="https://github.com/user-attachments/assets/bc3a3c3d-2e85-421a-a47a-1a63322074de" />




MODULE 2 (State and Memory):

  Lesson 1(State Schema): This notebook is like learning different ways to organize information for a school project.
      It shows three methods:
      TypedDict - like making a simple list with categories
      Dataclass - like creating a more organized form with sections
      The mai difference between TypeDict and Dataclas is that we use "state.name" for dataclass and state["name"] for typedict for accessing the values.
      Pydantic - like having a teacher check your work to make sure everything is correct
      The notebook builds a small program which takes a name, adds some text, and randomly decides if the mood is happy or sad - showing how each method keeps             track of this information differently.
      
   Tweaking: After experimenting with the state schema implementation, I customized the PydanticState class by changing the mood options from the original              "happy/sad" to "excited/tired" to better reflect different energy states. I also modified the probability logic in the decide_mood() function to create an           80/20 split favoring excitement over tiredness. Additionally, I enhanced the state schema by introducing new fields including an "energy_level" integer to          track vitality and a "message" string to store dynamic responses, making the graph's behavior more interactive and personalized.



   Lesson 2(State Reducers): When we build graphs where multiple parts run at the same time, this might try to change the same information, which causes problem.           State reducers are like rules that tell our program how they will combine these changes properly, like adding to a list instead of just overwriting. We can         use simple built-in reducers or create our own custom ones for special situations. Custom reducers are great because they let me handle tricky situations,          like when data is empty or needs a special way to be combined This is especially useful when working with chat messages where we need to add,                       update, or remove messages without causing conflicts.

   Tweaking: I started with a game scoring system which was giving errors when trying to add bonus points and subtract penalty points at the same time. The program        did not know which calculation to do first. So I created a special subtraction rule called a reducer that properly handles score that changes. Then I made          it even smarter to work even when starting without any score. When I tested it with an empty score and added 15 points, it correctly gave me a final score          of 15 points without any errors.




   Lesson 3(Multiple schemas): This lesson explains how to build workflows using LangGraph with different types of data schemas. It shows that normally all parts          of a workflow share one data structure, but sometimes we want more control. The notebook teaches two main tricks: using private data that only some steps           can see, and creating separate input/output formats to control what information goes in and comes out of the workflow. These techniques help organize               complex programs better by hiding unnecessary details and focusing on what's important.
   
   Tweakink: I changed the addition example to subtraction to make it more interesting and i was enjoying doing this. Instead of just adding numbers, the code i           wrote  will now subtract values and will even prevent negative results. I used different variable names like "final_result" and "starting_number" to make it        clearer what's happening. The workflow still follows the same steps but now does subtraction calculations instead. When I tested it with the number 25, it          gave me 12 as the final answer, and when I used 5, it gave me 0 since it doesn't allow negative numbers.Here, I tested with both the methods, private data          as well as with creating separate i/o formats.            

        



   Lesson 4(Trim and Filter Messages):This Lesson is all about learning how to manage conversation history in chatbots. It shows different ways to handle long             conversations so they don't get too big or slow. One method is filtering, where we will only keep the most recent messages and in the output we will only           see thr changes made int the recent message:                                                                                                                             <img width="1901" height="901" alt="image" src="https://github.com/user-attachments/assets/c286b06f-0346-43f1-93aa-ea4023619b8c" />                            Another is trimming, where we will limit the total number of words being used.It is based upon number of tokens,it restricts to specified number of tokens.              <img width="1897" height="909" alt="image" src="https://github.com/user-attachments/assets/cdb18ee2-cebd-477f-bf85-0f594df81563" />                            The Lesson uses examples about ocean animals to demonstrate these techniques, showing how the chatbot can remember just enough of the conversation to give          good answers without getting overloaded.

   Tweaking: I changed the example from ocean animals to multiplication maths problems. Instead of asking about whales and dolphins, I made the chatbot help with          times tables and multiplication questions. I kept the same filtering and trimming techniques but adjusted them for math conversations - keeping more                messages for better learning context. The chatbot now answers questions like "What is 6 times 7?" and helps students practice their multiplication skills           while managing the conversation history properly.                                                                                                                 When I ran the code, the chatbot correctly answered all the multiplication problems - it said 6×7=42, 8×9=72, 12×12=144, and 15×4=60. It also explained that         multiplication is repeated addition and encouraged the student to keep practicing, showing it remembered the math context despite the message filtering.           <img width="1790" height="914" alt="image" src="https://github.com/user-attachments/assets/20155571-36f8-47e8-9cea-cba0977f1d47" />                                 <img width="1808" height="891" alt="image" src="https://github.com/user-attachments/assets/e1dd9d49-16cc-4c21-bdae-b24674bf61b5" />                                 <img width="1850" height="879" alt="image" src="https://github.com/user-attachments/assets/63179efe-4a7d-4809-b165-1861dd00fb3a" />                                 <img width="1911" height="890" alt="image" src="https://github.com/user-attachments/assets/7ac06845-2732-4b1c-bf73-64b05ea27f03" />    


   Lesson 5(Summarizing messages and memory): This Lesson shows how to build a smart chatbot that can remember long conversations without getting too big.      Instead of just cutting off old messages, it creates summaries of the chat so far. The chatbot uses these summaries to understand what you talked about before, even if the conversation gets really long like here in the example we have set that if the length of the messages exceeds 6 the it will provide us the summary of the full conversation we did before. It also has memory that saves your chat history using threads,it is kind of like different chat channels. This way, the chatbot can pick up where you left off and keep track of your interests, like when someone talked about football players and the bot remembered their name and favorite team.                                                                                                                                                        <img width="1489" height="842" alt="image" src="https://github.com/user-attachments/assets/a4feacaf-383c-4921-b1f3-91f1bed19a5e" />                                <img width="1484" height="879" alt="image" src="https://github.com/user-attachments/assets/e7e6f7c6-4d98-48e8-af75-07b3e36766af" />

