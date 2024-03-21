title:: Novelty-based Intrusion Detection of Sensor Attacks on Unmanned Aerial Vehicles
file:: [whelan2020_1710759980610_0.pdf](../assets/whelan2020_1710759980610_0.pdf)
file-path:: ../assets/whelan2020_1710759980610_0.pdf

- ![Novelty-based Intrusion Detection of Sensor Attacks on Unmanned Aerial Vehicles](../assets/whelan2020_1710759980610_0.pdf)
- Dataset: https://ieee-dataport.org/open-access/uav-attack-dataset
- # Summary
	- Novelty-based approach to intrusion detection, using *one-class classifiers*.
	- One-class classifiers require only non-anomalous data to exist in training set => allows for the use of flight-logs as training data.
	- GPS spoofing is used in paper as common example of external sensor-based attack.
	- > Novelty detection, rather than anomaly detection, provides ability to learn from a training dataset where anomalies are not present.
	- **Contributions**:
		- Propose use of one-class novelty detection techniques for intrusion detection.
		- Discuss how one-class classifiers can be used to solve unavailability of labelled UAV intrusion detection datasets.
		- Demonstrate performance of various classifiers using data from simulated flights.
- # Methodology
	- **Pre-Processing:**
		- Features unique to components or sensors are clustered and separate models are trained for each cluster. Unrelated or autopilot-specific features are dropped (for universality).
		- Flight logs split into multiple CSVs based on sensor/topic logged.
		- *Interpolate values* for topics that are being polled at slower rate.
		- [[Principal Component Analysis]] is performed transform set of features into principal components to better explain variance in original set.
	- **Training and Tuning:**
		-