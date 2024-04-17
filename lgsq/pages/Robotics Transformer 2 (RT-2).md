url:: https://deepmind.google/discover/blog/rt-2-new-model-translates-vision-and-language-into-action/
link:: https://robotics-transformer2.github.io/
file:: [rt2.pdf](../assets/rt2_1713266786953_0.pdf)
published:: [[Jul 28th, 2023]]

- # Introduction
	- #+BEGIN_QUOTE
	  Robotic Transformer 2 (RT-2) is a novel vision-language-action (VLA) model that learns from both web and robotics data, and translates this knowledge into generalised instructions for robotic control
	  #+END_QUOTE
	- High capacity VLMs (Vision Language Model) are trained on web-scale datasets. This makes them good at recognising visual or language patterns across different languages.
	- For robots, achieving similar level of competency would require robot data first hand, across:
		- every object
		- every environment
		- every task
		- every situation
	- RT-2 is novel VLA model that learns from web and robotics data and translates this knowledge into generalised instructions for robotic control while maintaining web-scale capabilities.
	- [RT-1](https://research.google/blog/rt-1-robotics-transformer-for-real-world-control-at-scale/): trained on multi-task demonstrations, which can learn combinations of tasks and objects seen in the robotic data.
		- Builds on this.
		- Uses the robot demonstration data collected with 13 robots over 17 months in an office kitchen environment.
	- RT-2 shows:
		- improved generalisation capabilities,
		- semantic and visual understanding beyond exposed robotic data,
		- ability to interpret new commands and respond to user commands by performing rudimentary reasoning (reasoning about object categories or high-level descriptions).
	- Incorporates chain-of-thought reasoning, allowing RT-2 to perform multi-stage semantic reasoning.
- # VLMs -> Robotics
	- RT-2 builds on VLMs that take >1 images as input and produce sequence of tokens that represent natural language text.
	- RT-2 uses Pathways Language and Image model (PaLI-X) and Pathways Language model Embodied (PaLM-E) as its backbone.
	- *Robotic actions => Tokens*; Actions are described as strings that can be processed by standard natural language tokenisers.
	- ![](https://lh3.googleusercontent.com/kXU5F9WVMd1eaTuwwU-QB3HbbDy1A6YPZQ-kdM65mRCpFwNgNEp34xJrfqW60iQYtBhxfBWuGNex8RoEOTR4_oDpJv_Qj4tUp0A_WcFTch5aJ-QD=w1070)
	- |>This string could be represented with token numbers eg: "1 128 91 241 5 101 127 217"
	- **RT-2 Architecture and Training:**
		- Co-fine-tune a pre-trained VLM on robotics and web data.
		- Resulting model takes in robot camera images and directly predicts actions for robot to perform.
- # Generalisation and Emergent Skills
	- 6000 robotic trials - qualitative and quantitative experiments
	- Three categories of skills:
		- Symbol understanding,
		- Reasoning,
		- Human Recognition.
	- When asked to perform tasks not seen in robotic data, requires translated knowledge from web-data to operate.
		- "put *strawberry* into the *correct bowl*"
		- "pick *land animal*"
		- "pick *animal* with *different colour*"
		- etc.
	- ![success rates of emergent skill evaluations](https://lh3.googleusercontent.com/4yaN_bq7MT1gaQ3ebf0hutNQAdm5an_tCJ_8PEeZla9mu4nKyTJfdYIQl9cgp0GwTjQNjZL_8lGt3IlzjGe7TKr8lNZs6yq8cYmX1fMk7gfOa1wvkw=w1232-rw)
		- Observed more than 3x improvement in generalisation performance compared to RT-1 and Visual Cortex (VC-1)
	- ![](https://deepmind.google/api/blob/website/images/64c28bb0a7e46157ca3edb96_64c2566864b91d6bd0590f.original_SdQBLUz.svg)
		- 62% improved performance on previously unseen scenarios
	- Probed RT-2 to combine **robotic control** with **chain-of-thought reasoning** to enable **long-horizon planning**.
		- Variant of RT-2 tuned to few hundred gradient steps to increase ability to use language and actions jointly.
		- Augmented data to include additional "Plan" step: (1) Describe purpose of action; (2) "Action" in action tokens.
		- ![unnamed.webp](https://lh3.googleusercontent.com/b-Rfo69ZIkh3cwd_Flyniskrza5l7P-VI1zknpxd8Z_tqR-GB25b_9eN0tFX3k6wKeyTW5MFOzXC24GCiBWaMvcNZnI_Q0cVGIM-fyEVWOn_Xx6J=w1232-rw)
	- RT-2 can use both **image and text commands**.
- # Summary
	- VLMs can be transformed into powerful VLA models to directly control robot by combining VLM pre-training with robotic data.
	- PaLM-E /\ PaLI-X -> VLA => improved robotic policies, and significantly better generalisation performance and emergent capabilities inherited from web-scale vision-language pre-training.