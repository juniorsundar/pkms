# Definition
	- In machine learning models, feature importance refers to methods of assigning scores to input features. These scores represent how significant each feature is in influencing the model's predictions.
	- Feature importance allows you to:
		- **Improve understanding** - Recognise key factors driving a model's decisions.
		- **Reduce dimensionality** - Remove irrelevant or redundant features to streamline models.
		- **Debug models** - Identify features that may be negatively impacting performance.
- # Common Techniques
	- ## Impurity-based feature importance (Decision Trees, Random Forests)
		- Calculates the reduction in node impurity (e.g. [[Gini Impurity]], Entropy) brought about by each feature split across all trees in an ensemble. *Features that lead to larger impurity reductions are deemed more important*.
		- It is built-in to decision tree-based methods, and is computationally efficient.
		- It can be biased towards features with more categories or continuous features.
	- ## Permutation importance
		- For each feature, its values are randomly shuffled, and the decrease in model performance (e.g. accuracy decline) is measured. Features leading to a larger drop in performance when shuffled are considered more important.
		- It is model-agnostic, and also considers feature interactions.
		- It is computationally more expensive than impurity-based importance.
	- ## Sensitivity analysis
		- Measures how small changes in individual features impact the model's output. Largest changes in output indicate higher feature importance.
		- It provides insight into the direction of the feature's impact (positive or negative).
		- Computationally intensive, especially with large number of features.
	- ## SHAP (SHapley Additive exPlanations)
		- Model-agnostic method based on game theory. Uses Shapley values to determine the fair distribution of attribution of a prediction to each feature.
		- Considers feature interactions and can handle feature dependence, provides global and local explanations.
		- It is computationally expensive.
- # Technique Selection
	- **Model Type** - If you're using decision tress or tree ensembles, impurity-base importance is a natural choice. Otherwise, SHAP or permutation importance are more versatile.
	- **Computation Cost** - Permutation importance and SHAP can be slower, especially for a large dataset. If speed is crucial, impurity-based or sensitivity analysis might be better.
	- **Need for Global vs. Local Explanations** - SHAP is excellent for both understanding features' overall importance and for explaining individual predictions.
- # Libraries for Implementation
	- `scikit-learn` (Python) - Provides impurity-based importance for tree models, permutation importance, and limited partial dependence plots of sensitivity.
	- `SHAP` (Python) - A powerful library specifically designed for calculating SHAP values.