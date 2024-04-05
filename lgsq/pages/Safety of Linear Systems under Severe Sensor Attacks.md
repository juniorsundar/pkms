title:: Safety of Linear Systems under Severe Sensor Attacks
file:: ![Safety of Linear Systems under Severe Sensor Attacks](../assets/tan2024_1712303317274_0.pdf)
file-path:: ../assets/tan2024_1712303317274_0.pdf

- # Summary
	- Attacked is omniscient and can spoof several system sensors at will.
	- Existing results have derived necessary and sufficient conditions under which the state estimation problem has a unique solution.
	- This paper considers severe attacking scenario when such conditions do not hold.
	- Derive exact characterisation of set of all possible state estimates.
	- Use framework of [[Control Barrier Functions]] to propose design principles for system safety in offline and online phases.
		- **Offline phase** - derive conditions on safe sets for all possible sensor attacks encounterable during system deployments.
		- **Online phase** - quadratic program-based safety filter is proposed to enforce system safety.
	- Illustrated with 2D-vehicle example.
	- Only theoretical results.
- # Introduction
	- In this paper:
		- certain measurements of CPS are compromised by attacker.
		- general attack model in setting of linear systems, imposes no limitations on the magnitude, statistical properties, or temporal evolution requirements on the attack signal.
		- only assuming upper bound on the number of attacked sensors.
	- Existing results focus on recovering system state from compromised measurement data (AKA secure state reconstruction problem).
	- To derive necessary and sufficient conditions to find unique solutions to this problem:
		- In discrete time linear system a condition is posed as a sparse observability property of CPS.
		- Equivalent condition for continuous time LS shows that finding unique solution is NP-hard in general.
	- > "can we ensure safety of the system, and thereby avoid catastrophic results through active control, even when certain sensors are compromised?"
		- Here, safety refers to the property to limit control system trajectories to remain with in a safe set via feedback
		- Compromised sensor measures negatively effect or mislead state estimates.
	- [[Control Barrier Functions]] have been applied to use cases of privacy preservation and safety in presence of faulty sensors. But in case of adversarial omniscient attacker, state estimation error does not satisfy assumptions of CBFs.
	- This work tries to patch this