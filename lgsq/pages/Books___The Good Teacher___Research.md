# Analytical Engine
	- ## Context
	  collapsed:: true
		- Design for a mechanical general-purpose computer by Charles Babbage in the 1830s.
		- Intended to be programmable and capable of performing a wide variety of calculations.
		- **Key Features**
		  collapsed:: true
			- **Arithmetic Logic Unit (ALU)**: Performs arithmetic and logical operations.
			- **Control Flow**: Includes conditional branching and loops for changing the sequence of operations and repeating instructions.
			- **Memory**: Stores data and intermediate results.
			- **Input and Output**: Methods for inputting data and instructions, and outputting results.
		- Was never completed, but it laid the foundation for modern computing.
	- ## Arcane Analytical Engine
	  id:: 666d36e1-b758-4344-b054-a0c3a5092887
	  collapsed:: true
		- ### Overview
		  collapsed:: true
			- A magical version of the Analytical Engine designed for mathematical and scientific calculations.
			- Central Mana Core obtained from a wisp, programmed with inscriptions.
			- Enchanted tablets act as memory storage.
		- ### Key Features
			- **Mana Core**: Central core inscribed with control runes and glyphs.
			- **Additional Core Structures**:
				- Memory storage (long and short term)
				- Compiler
			- **I/O:** via Means of inscribed tablets with gem embeds.
		- ### Control Flow
			- **Conditional Branching**:
				- Checks conditions and directs mana flow accordingly.
				- Example:
				  ```plaintext
				  if manaReserve > threshold then
				    status = "Sufficient";
				  else
				    status = "Low";
				  end if
				  ```
			- **Loops**:
				- Repeats a set of instructions until a condition is met.
				- Example:
				  ```plaintext
				  while manaReserve < 200 do
				    manaReserve = manaReserve + 10;
				  end while
				  ```
		- ### ArcaneScript: Pseudo Programming Language
			- **Variables**:
				- Declaration: `let <variable_name> = <value>;`
				- Example:
				  ```plaintext
				  let manaReserve = 100;
				  let result = 0;
				  ```
			- **Basic Operations**:
				- Addition: `+`
				- Subtraction: `-`
				- Multiplication: `*`
				- Division: `/`
				- Example:
				  ```plaintext
				  let sum = manaReserve + 50;
				  let product = manaReserve * 2;
				  ```
			- **Control Flow**:
				- Conditional Statements:
				  ```plaintext
				  if <condition> then
				    <instructions>
				  else
				    <instructions>
				  end if
				  ```
				- Loops:
				  ```plaintext
				  while <condition> do
				    <instructions>
				  end while
				  ```
			- **Functions**:
				- Mathematical and scientific functions.
				- Example:
				  ```plaintext
				  function square(x) {
				    return x * x;
				  }
				  
				  function factorial(n) {
				    let result = 1;
				    while n > 1 do
				      result = result * n;
				      n = n - 1;
				    end while
				    return result;
				  }
				  
				  let num = 5;
				  let fact = factorial(num);
				  let sqr = square(num);
				  ```
		- ### Compiler Design
			- **Lexical Analysis**:
				- Tokenization: Breaking down the script into tokens.
			- **Syntax Analysis**:
				- Parsing: Checking tokens against grammar rules.
			- **Semantic Analysis**:
				- Validation: Ensuring the script’s logic is correct.
			- **Intermediate Representation**:
				- Conversion: Translating the script into an intermediate arcane representation.
			- **Code Generation**:
				- Arcane Encoding: Converting intermediate representation into binary/arcane format.
			- **Optimization**:
				- Efficiency: Optimizing instructions for faster execution and minimal mana usage.
			- **Example Workflow**:
				- Input Script (ArcaneScript):
				  ```plaintext
				  let manaReserve = 100;
				  let threshold = 50;
				  let status = "Normal";
				  
				  if manaReserve > threshold then
				    status = "Sufficient";
				  else
				    status = "Low";
				  end if
				  
				  function square(x) {
				    return x * x;
				  }
				  
				  function factorial(n) {
				    let result = 1;
				    while n > 1 do
				      result = result * n;
				      n = n - 1;
				    end while
				    return result;
				  }
				  
				  let num = 5;
				  let fact = factorial(num);
				  let sqr = square(num);
				  ```
				- Lexical Analysis:
				  ```plaintext
				  ["let", "manaReserve", "=", "100", ";", "let", "threshold", "=", "50", ";", "let", "status", "=", "\"Normal\"", ";", "if", "manaReserve", ">", "threshold", "then", "status", "=", "\"Sufficient\"", ";", "else", "status", "=", "\"Low\"", ";", "end if", "function", "square", "(", "x", ")", "{", "return", "x", "*", "x", ";", "}", "function", "factorial", "(", "n", ")", "{", "let", "result", "=", "1", ";", "while", "n", ">", "1", "do", "result", "=", "result", "*", "n", ";", "n", "=", "n", "-", "1", ";", "end while", "return", "result", ";", "}", "let", "num", "=", "5", ";", "let", "fact", "=", "factorial", "(", "num", ")", ";", "let", "sqr", "=", "square", "(", "num", ")", ";"]
				  ```
				- Syntax Analysis:
					- Constructs a syntax tree from tokens.
				- Semantic Analysis:
					- Ensures logical consistency.
				- Intermediate Representation:
				  ```plaintext
				  [Assign "manaReserve" 100, Assign "threshold" 50, Assign "status" "Normal", If (Greater "manaReserve" "threshold") [Assign "status" "Sufficient"] [Assign "status" "Low"], Function "square" ["x"] [Return (Multiply "x" "x")], Function "factorial" ["n"] [Assign "result" 1, While (Greater "n" 1) [Assign "result" (Multiply "result" "n"), Assign "n" (Subtract "n" 1)], Return "result"], Assign "num" 5, Assign "fact" (Call "factorial" ["num"]), Assign "sqr" (Call "square" ["num"])]
				  ```
				- Code Generation:
				  ```plaintext
				  0001 0110 0110 0100 1000  // Assign manaReserve = 100
				  0001 0117 0110 0101 1010  // Assign threshold = 50
				  0001 1000 0110 0116 1101  // Assign status = "Normal"
				  0010 0001 0110 0100 0117 0117 0110 0101  // If manaReserve > threshold
				  0011 1000 0110 1000 0116 1011  // Assign status = "Sufficient"
				  0100 1000 0110 1001 0116 1110  // Else Assign status = "Low"
				  0101 1110  // End If
				  0110 0001 0117 0101  // Function square(x)
				  0117 0110 1001 0116 1111 0116 1001 0116 1101  // Return x * x
				  1000 0117  // End Function
				  1001 0001 0117 0000 0116 1001 0116 0117  // Function factorial(n)
				  1010 1001 0117 0011 0116 1101 0117 0001 0116 0116 0116 1010  // While n > 1
				  1011 1001 0117 0011 0116 0116 0116 1001 0116 1101  // Assign result = result * n
				  1100 0117 0116 0116 0116 1110 0116 1101  // Assign n = n - 1
				  1101 1110  // End While
				  1110 0116 0116 1011 0116 1110  // Return result
				  1111 0001  // End Function
				  0001 0116 0116 0117 0116 0116  // Assign num = 5
				  0001 1001 0116 0116 1000 0117 0116 1000 0116 1001 0116 1011  // Assign fact = factorial(num)
				  0001 1001 0116 0116 1010 0117 0116 1000 0116 1001 0116 1101  // Assign sqr = square(num)
				  ```
				- Optimization:
					- Optimizes the arcane code for efficiency and minimal mana use.
		- ### Example Workflow
			- **Programming**:
				- A user assembles pre-formed keyword blocks like "let" into sequence and stamps them onto a fixed-size tablet with a mana gem embedding.
					- #+BEGIN_WARNING
					  This is a limitation of first implementation. There isn’t a standardized input method like keyboard or mouse.
					  #+END_WARNING
				- The mana gem on the tablet captures the printed data via a simple parser.
					- #+BEGIN_WARNING
					  This is a limitation of first implementation. There is a limit to how much the compiler can parse the program.
					  #+END_WARNING
			- **Execution**:
				- The gem is transferred to another tablet with an empty gem and fed into the compiler arcane mechanism.
				- The compiler processes the gem and outputs a binary-type output into the output gem.
			- **Analytical Engine Processing**:
				- The output gem is fed into the Analytical Engine.
				- The engine processes the data and outputs the results onto a magnetized surface with iron shavings.
			- **Output**:
				- Results displayed on a magnetized surface with iron shavings.