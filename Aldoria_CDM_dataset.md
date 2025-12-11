This dataset is a collection of **Conjunction Data Messages (CDMs)**. These are standardized reports used in the space industry to warn satellite operators about potential collisions between space objects (satellites and space debris).

***

### Dataset Overview: Aldoria Conjunction Data Messages (CDM)

**1. Introduction**
This dataset, sourced from **Aldoria**, contains Conjunction Data Messages (CDMs). These records are the industry standard for Space Situational Awareness (SSA), used to predict and analyze close approaches (conjunctions) between two objects in orbit. The data provides orbital geometry, uncertainty, and collision risk at the Time of Closest Approach (TCA).

**2. Data Structure & Content**
The dataset features pairs of space objects, designated as **Object 1** (typically the asset or payload of interest) and **Object 2** (typically the secondary object, often debris or another payload). The features can be categorized into four distinct domains:

* **Identity & Metadata:** Identifiers (`international_designator`, `catalog_name`), object types, and creation dates.
* **State Vectors (Kinematics):** Position ($x, y, z$) and Velocity ($\dot{x}, \dot{y}, \dot{z}$) components relative to a reference frame, defining the precise location of the objects.
* **Covariance (Uncertainty):** A comprehensive set of covariance matrix elements (e.g., `c_r_r`, `c_n_t`) which quantify the uncertainty in the position and velocity measurements. This is critical for calculating probability.
* **Risk Metrics:** Calculated values representing the severity of the event, including:
    * `collision_probability`: The likelihood of impact.
    * `miss_distance`: The absolute distance between objects at the closest point.
    * `relative_speed` & `relative_velocity`: How fast the objects are moving past one another.

* **The "Maneuverability" Gap:** The significant missing data is found in `object1_maneuverable` and `object2_maneuverable`, which are both missing approximately **80.5%** of their values.
    * *Domain Insight:* This high missingness is expected in SSA data. Object 2 is frequently "space debris" or a non-active object for which maneuverability status is unknown or undefined. Similarly, if Object 1 is not the operator's own satellite, its capabilities may not be public record in the CDM context.

**4. Utility**
This dataset is suitable for:
* Training Machine Learning models to predict collision risk (using the state vectors and covariance).
* Analyzing the frequency and distribution of high-risk conjunction events.
* Validating collision probability algorithms.


