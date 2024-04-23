url:: https://www.microsoft.com/en-us/research/group/autonomous-systems-group-robotics/articles/chatgpt-for-robotics/
file:: [chatgpt-robotics.pdf](../assets/chatgpt-robotics_1713333848816_0.pdf)
published:: [[Feb 20th, 2023]]

- **IMPORTANT:** Paper written in large part with the help of ChatGPT
- # Introduction
	- Extended capabilities of ChatGPT to robotics beacuse,
		- it incorporates strengths of natural language and code generation models along with flexibility of dialogue.
		- can engage in free-form dialogue, with long context, to interact in a more natural fashion.
	- Intuitively controlled multiple platforms such as robot arms, drones, and home assistant robots with language.
	- **Key problem:** Teaching ChatGPT to solve problems considering...
		- ...laws of physics,
		- ...context of operating environment,
		- ...how robot's physical actions affect state of the world.
	- ## Zero-Shot Learning
		- Technique to enable robot or models to generalise their knowledge and perform tasks they are not explicitly trained for.
		- Achieved by transforming knowledge from seen classes to unseen classes through embedding space or feature generation.
	- ## Process
		- Create an interfacing layer between user intention and robotic control.
		- The interfacing layer is a library of high-level functions that ChatGPT will deal with directly.
		- The layer then deals with the back-end to the actual APIs for the platform of choice.
	- ## Contributions
		- Demonstrate pipeline for applying ChatGPT to robotic tasks with several prompting techniques:
			- free-form natural language dialogue,
			- code-prompting,
			- XML tags,
			- Closed-loop reasoning.
		- Evaluate (experimentally) ChatGPT's ability to execute robotic tasks. In simulated and real-world experiments, show ability to solve:
			- mathematical operations,
			- local operations,
			- geometrical operations,
			- more complex scenarios with embodied agents, UAVs, and robotic arms.
		- Introduce [PromptCraft](https://github.com/microsoft/PromptCraft-Robotics) as a collaborative prompt engineering platform.
		- Release simulation tool on top of Microsoft AirSim with ChatGPT integration (AirSim-ChatGPT).
- # Design Principles
	- Define a high-level robot function library:
		- can be specific to a form factor or use-case, and maps to actual implementations on robotic platform.
		- must be descriptively named for ChatGPT to understand.
	- Build prompt which:
		- describes objective while identifying set of high-level functions in library.
		- can contain information about constraints, or info on how to structure responses.
	- User staying *on* the loop to evaluate code output, and provide feedback to ChatGPT on quality and safety.
	- Iterate on generated implementation then deploy on robot.
- # Good Prompting Practices
	- Constraints and requirements
	- Environment
	- Current state
	- Goals and objectives
	- (OPTIONAL) Solution example
	- (OPTIONAL) Direct ChatGPT to respond in XML to aid code-parsing or even understanding (eg. <question></question> <cmd></cmd> <reason></reason>)