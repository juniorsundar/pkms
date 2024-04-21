title:: Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving
file:: [Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving](../assets/shoukry2015_1713459757385_0.pdf)
file-path:: ../assets/shoukry2015_1713459757385_0.pdf

- # Introduction
	- > What is Satisfiability Modulo Theory?
	- Stuxnet virus targeting SCADA systems --> Feeds previously recorded measurements back into the controller.
	- *Secure state reconstruction* is process of reconstructing actual system states by using data collected from attack-free sensors.
		- No assumptions are made about the attack, such as the stochastic properties, time evolution, or energy bounds.
		- Has been attempted mainly in linear systems, this paper approaches this topic in nonlinear space.
		- More specifically, it looks at physical systems that are differentially flat.
	- > What does it mean when a system is scalar?
	- **As long as knowledge of system state is available** differentially flat systems can be converted into linear systems using:
		- dynamic feedback linearisation, and
		- a change of coordinates
	- The condition for state reconstruction is that the system is [s-sparse observable](((66241c81-a768-4349-992a-6ff66e19737b))).
- # Differentially Flat Systems
	- System is differentially flat if the state and the input can be reconstructed from current and previous outputs.
	- ## Formal Definition
		- System is differentially flat if there exists an integer $k\in \mathbb{N}$, and functions $\alpha$ and $\beta$, such that the state and the input can be reconstructed from the outputs $y^{(t)}$ as follows:
		- $$x^{(t)} = \alpha (y^{(t)}, y^{(t-1)}, \dots , y^{(t-k+1)})$$
		- $$u^{(t)} = \beta (y^{(t)}, y^{(t-1)}, \dots , y^{(t-k+1)})$$
		- In such cases, the output $y(t)$ is called a flat output.
	- ## s-Sparse Flat Systems
		- Nonlinear control system $\Sigma_a$:
		- $$\Sigma_a \biggl\{ \frac{ x^{(t+1)} = f(x^{(t)}, u^{(t)})}{ y^{(t)} = h(x^{(t)}) + a^{(t)}}$$
		- #+BEGIN_TIP
		  Here, $a^{(t)}$ is the attack vector which is s-sparse, such that if sensors $i\in \{1,\dots,p\}$ is attacked then the $i$th component of the vector is non-zero.
		  #+END_TIP
		- is said to be s-sparse flat if for every set $\Gamma \subseteq \{1, \dots, p\}$ with $|\Gamma|=s$, the system $\Sigma_{\bar{\Gamma}}$:
		- $$\Sigma_{\bar{\Gamma}} \biggl\{ \frac{ x^{(t+1)} = f(x^{(t)}, u^{(t)})}{ y^{(t)} = h_{\bar{\Gamma}}(x^{(t)})}$$
		- is differentially flat.
		- In other words, the system is s-sparse flat if any choice of $p-s$ sensors is a flat output.