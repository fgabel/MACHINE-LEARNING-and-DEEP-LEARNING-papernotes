# [The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/aad9f93b86b7addfea4c419b9100c6cdd26cacea.pdf)

In this paper summary, I will explain some background in the notes below, so if you are unfamiliar with some terms, there is a good chance it is explained in the *notes* section.

**Problem**: 
- Creating reliable, production-level machine learning systems brings on a host of concerns not found in
small toy examples or even large offline research experiments.
- To get a ML system ready for production and to reduce its technical debt, testing and monitoring are key considerations. It is, however, unclear how to formulate specific tests.

 **Solution**: 
 - This paper identifies 28 specific tests and monitoring needs, drawn from experience with a wide range of production ML systems to help quantify these issues and present an easy to follow road-map to improve production readiness and pay down ML technical debt.
 - Hereby, the paper operates on the intersection of software testing and machine learning, both very well studied but their intersection has been less well explored in the literature.

**28 specific test and monitoring needs**

-  **1: Feature expectations are captured in a schema**: It is useful to encode intuitions about the data in a schema so they can be automatically checked. For example, an adult human is surely between one and ten feet in height. Such expectations can be used for tests on input data during training and serving. One approach to generate such an expectation schema would be to start with calculating statistics from training data, and use domain knowledge to adjust them.
-  **2: All features are beneficial**: This relates to scenarios where researchers are in a situation to add and remove features. It often makes sense to keep models sparse by, e.g., calculating correlation coefficients.
- **3: No feature’s cost is too much:** Again, adding too many features might have implications on RAM usage, inference latency, and upstream data dependencies.
**Notes**:
* Technical debt is a common computer science metaohor for the possible consequences of poor technical implementation of software. It can very much be compared to monetary debt. If technical debt is not repaid, it can accumulate 'interest', making it harder to implement changes later on. 
