Discussion and Reflection
The bulk of this project consists of a collection of five questions. You are to answer these questions after spending some amount of time looking over the code together to gather answers for your questions. Try to seriously dig into the project together--it is of course understood that you may not grasp every detail, but put forth serious effort to spend several hours reading and discussing the code, along with anything you have taken from it.
Questions will largely be graded on completion and maturity, but the instructors do reserve the right to take off for technical inaccuracies (i.e., if you say something factually wrong).
Each of these (six, five main followed by last) questions should take roughly at least a paragraph or two. Try to aim for between 1-500 words per question. You may divide up the work, but each of you should collectively read and agree to each other's answers.
[ Question 1 ]
For this task, you will three new .irv programs. These are ir-virtual? programs in a pseudo-assembly format. Try to compile the program. Here, you should briefly explain the purpose of ir-virtual, especially how it is different than x86: what are the pros and cons of using ir-virtual as a representation? You can get the compiler to to compile ir-virtual files like so:
racket compiler.rkt -v test-programs/sum1.irv
(Also pass in -m for Mac)
Ir-virtual is an intermediate representation (IR) int he compilation process. The purpose of ir-virtual is to serve as the middleman between the source code and the hardware instructions. It can be viewed as a translator that helps the compiler understand the program’s logic regardless of the type of computer. Compared to x86, ir-virtual is more flexible and portable. The abstraction of ir-virtual has both positive and negative effects: it is able to facilitate optimizations and transformations without being tied to the specific architecture, but it is not as efficient since the code is not optimized for the target architecture. 
[ Question 2 ]
For this task, you will write three new .ifa programs. Your programs must be correct, in the sense that they are valid. There are a set of starter programs in the test-programs directory now. Your job is to create three new .ifa programs and compile and run each of them. It is very much possible that the compiler will be broken: part of your exercise is identifying if you can find any possible bugs in the compiler.
For each of your exercises, write here what the input and output was from the compiler. Read through each of the phases, by passing in the-v flag to the compiler. For at least one of the programs, explain carefully the relevance of each of the intermediate representations.
three programs: (if #t
    (print (+ 1 2)))

(let* [x (+ 1 2)] [y (* x 2)] [z (+ y 1)] [w (/ z 2)] (print w))

(if (<= 5 10)
    (let* [a #t] [b #f] (print a)))

[ Question 3 ]
Describe each of the passes of the compiler in a slight degree of detail, using specific examples to discuss what each pass does. The compiler is designed in series of layers, with each higher-level IR desugaring to a lower-level IR until ultimately arriving at x86-64 assembler. Do you think there are any redundant passes? Do you think there could be more?
In answering this question, you must use specific examples that you got from running the compiler and generating an output.
Each step in the compiler's process plays a crucial role in turning source code into executable x86-64 assembler. The process starts off with IfArith and progresses through IfArithTiny, ANF, IR-Virtual, and finally x86 assembly. Each step simplifies or optimizes the code in a specific way. For example, IfArith to IfArithTiny removes complex constructs like let* to make the code easier to handle. ANF then normalizes the code by breaking down complex expressions and introducing administrative bindings. This makes the code uniform and easier to optimize later. IR-Virtual simplifies the code further, expressing instructions in virtual registers and basic operations. Finally, x86 assembly translates the code into machine language. While each step serves a purpose, the overall process is redundant and can be more concise. For instance, merging IfArith to IfArithTiny with ANF could streamline the process. Additionally, adding more optimization passes could boost the code's efficiency, but balance is crucial to maintain speed and effectiveness.

[ Question 4 ]
This is a larger project, compared to our previous projects. This project uses a large combination of idioms: tail recursion, folds, etc.. Discuss a few programming idioms that you can identify in the project that we discussed in class this semester. There is no specific definition of what an idiom is: think carefully about whether you see any pattern in this code that resonates with you from earlier in the semester.
	One prevalent programming idiom in this project is pattern matching, specifically match cases. Pattern matching allows for selective extraction of data from lists and algebraic data types. By defining cases for speciifc patterns, we are able to concisely handle scenarios within the functions.
Another programming idiom can be described through the usage of logical operators. Logical operators such as “&&” and “!” are commonly used to combine and evaluate Boolean expressions. For example, these operators can be used to combine conditions to determine whether a specific element can be included in the result. 
[ Question 5 ]
In this question, you will play the role of bug finder. I would like you to be creative, adversarial, and exploratory. Spend an hour or two looking throughout the code and try to break it. Try to see if you can identify a buggy program: a program that should work, but does not. This could either be that the compiler crashes, or it could be that it produces code which will not assemble. Last, even if the code assembles and links, its behavior could be incorrect.
To answer this question, I want you to summarize your discussion, experiences, and findings by adversarily breaking the compiler. If there is something you think should work (but does not), feel free to ask me.
Your team will receive a small bonus for being the first team to report a unique bug (unique determined by me).
[ High Level Reflection ]
In roughly 100-500 words, write a summary of your findings in working on this project: what did you learn, what did you find interesting, what did you find challenging? As you progress in your career, it will be increasingly important to have technical conversations about the nuts and bolts of code, try to use this experience as a way to think about how you would approach doing group code critique. What would you do differently next time, what did you learn?


