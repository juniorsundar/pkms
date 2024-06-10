title:: Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving
file:: [Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving](../assets/shoukry2015_1713459757385_0.pdf)
file-path:: ../assets/shoukry2015_1713459757385_0.pdf

- # Introduction
	- Stuxnet virus targeting SCADA systems --> Feeds previously recorded measurements back into the controller.
	- *Secure state reconstruction* is process of reconstructing actual system states by using data collected from attack-free sensors.
		- No assumptions are made about the attack, such as the stochastic properties, time evolution, or energy bounds.
		- Has been attempted mainly in linear systems, this paper approaches this topic in nonlinear space.
		- More specifically, it looks at physical systems that are differentially flat.
	- **Scalar system** is a system whose variables and parameters are scalar quantities rather than vectors or matrices.
	- **As long as knowledge of system state is available** differentially flat systems can be converted into linear systems using:
		- dynamic feedback linearisation, and
		- a change of coordinates
	- The condition for state reconstruction is that the system is [s-sparse observable](((66241c81-a768-4349-992a-6ff66e19737b))).
	- {{embed [[Differentially Flat Systems]]}}
- # Secure State Reconstruction using SMT Solving
	- Assumes knowledge of [[Satisfiability Modulo Theory]].
	- Secure state reconstruction problem is combinatorial, since direct solution will require constructing the state from all different combinations of $p-\bar{s}$ sensors to determine which sensors are under attack.
- # Case Study: Securing Quadrotor Mission
	- Quadrotor takes-off an moves in a flat square trajectory.
	- Two IMUs, one of which has its vertical velocity reading attacked with a sinusoid on top of actual reading.
	- Only attacked on two parallel sides (not the whole trajectory).
	- A system model approximation is necessary.
	- Controller designed to be robust against bounded perturbations.
- # Conclusion
	- Given upper bound $\bar{s}$ on number of attacked sensors, it is showed that $2\bar{s}$-sparse flatness is sufficient condition for state reconstruction in spite of attack.
	- SMT based detection algorithm for differentially flat systems proposed.