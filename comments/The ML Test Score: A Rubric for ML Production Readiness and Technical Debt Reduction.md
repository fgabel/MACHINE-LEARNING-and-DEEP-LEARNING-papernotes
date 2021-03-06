# [The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/aad9f93b86b7addfea4c419b9100c6cdd26cacea.pdf)

In this paper summary, I will explain some background in the notes below, so if you are unfamiliar with some terms, there is a good chance it is explained in the *notes* section.

**Problem**: 
- Creating reliable, production-level machine learning systems brings on a host of concerns not found in
small toy examples or even large offline research experiments.
- To get a ML system ready for production and to reduce its technical debt, testing and monitoring are key considerations. It is, however, unclear how to formulate specific tests.
- ML/DL models are a function of data and models, so practices from building reliable software need to be transferred to both the data side and the model side.

 **Solution**: 
 - This paper identifies 28 specific tests and monitoring needs, drawn from experience with a wide range of production ML systems to help quantify these issues and present an easy to follow road-map to improve production readiness and pay down ML technical debt.
 - Hereby, the paper operates on the intersection of software testing and machine learning, both very well studied but their intersection has been less well explored in the literature.

**28 specific test and monitoring needs**

-  *DATA* **1: Feature expectations are captured in a schema**: It is useful to encode intuitions about the data in a schema so they can be automatically checked. For example, an adult human is surely between one and ten feet in height. Such expectations can be used for tests on input data during training and serving. One approach to generate such an expectation schema would be to start with calculating statistics from training data, and use domain knowledge to adjust them.
-  *DATA* **2&3: Are all features are beneficial and what's the cost of additional features?**: This relates to scenarios where researchers are in a situation to add and remove features. It often makes sense to keep models sparse by, e.g., calculating correlation coefficients. Also, adding too many features might have implications on RAM usage, inference latency, and upstream data dependencies. 
- *DATA* **4&5: Features adhere to meta-level requirements:** Programmatically ensure that e.g. data protection is adhered to by design and make sure that things like the "right to forget" makes its way into the ML pipeline.
- *DATA* **6: New features can be added quickly:** Make sure that new features and data can be added to a model swiftly even in production. This entails an efficient validation scheme and also infrastructural needs. Might conflict with privacy needs (4&5)!
- *DATA* **7: Test of input feature code:** Testing code that is responsible for integrating data/features or models into the codebase needs to be tested thorougly.

- *MODELS* **1: Code review and version control** Mostly for reasons related to debugging and reproducibility, code needs to be thoroughly reviewed and check into a repository so that it's clear what code has been run with which data at any point in the future.
- *MODELS* **2: Offline proxy metrics correlate with actual online impact metrics** This relates to the fact that optimized metrics (the loss) need to strongly correlate with improvements in user-facing outcomes.
- *MODELS* **3: Hyperparemeters** Hyperparameter tuning is often very effective. Efforts towards this need to be streamlined and justified to save resources and time.
- *MODELS* **4: Model staleness** Rapidly changing models (most often due to incoming training data) make deployed models stale (out-dated) quickly. There needs to be a robust validation strategy to learn about the impact of changing training data on models, e.g. using A/B-testing.
- *MODELS* **5: Testing against a simple model** Getting baseline predictions from a simple model helps confirming the usefulness of a whole pipeline.
- *MODELS* **6:Model quality is sufficient on all important data slices** Subsetting data and checking performance on this *slice* might help find corner cases that are not covered by the training data distribution.
- *MODELS* **7: Bias in training data** It's an empirical fact that ML models tend to be biased (learned from training data). Getting rid of this bias is not trivial and involves an accurate specification of an expected distribution of data along certain dimensions. For example, in an automated driving object detection scenario, certain classes might be underrepresented and thereby not learned at all.
- *INFRASTRUCTURE* **1: Reproducible Training** Ensuring determinism helps with auditing and tracking errors. However, this is hard, and even seeding (of RNG operations) and tracking training data order might not help as not every operation is guaranteed to be atomic in multi-threaded environments.
- *INFRASTRUCTURE* **2: Unit Tests in model specification code** This relates to algorithmic correctness of involved libraries (testable by feeding random input data and performing one epoch of training) as well as ML APIs (this is harder to test and involves e.g. performing assertions on subcomputations like single RNN cells or similar).
- *INFRASTRUCTURE* **3: Integration test of the full ML pipeline** A complete ML pipeline typically consists of assembling
training data, feature generation, model training, model verification, and deployment to a serving system. Each of these steps can introduce errors. Therefore, there should, for example, be an automated test spanning the whole pipeline as opposed to many single ones.
- *INFRASTRUCTURE* **4: Validation before production readiness** Before a model can reach production, it must automatically be validated for sufficient quality - it is important to test for both slow degradations in quality over many versions as well as sudden drops in predictive performance.
a new version.
**Notes**:
* Technical debt is a common computer science metaohor for the possible consequences of poor technical implementation of software. It can very much be compared to monetary debt. If technical debt is not repaid, it can accumulate 'interest', making it harder to implement changes later on. 

