# Fairness - Tradeoffs

## [Fair prediction with disparate impact: A study of bias in recidivism prediction instruments](https://arxiv.org/pdf/1610.07524)

## Introduction and Motivation

Recidivism Prediction Instruments (RPIs) are widely used in the criminal justice system to assess the likelihood of reoffending, influencing decisions on bail, parole, and sentencing. While RPIs aim to provide objective data-driven assessments, they have faced criticism for potential biases, particularly concerning race.

ProPublica's investigation into the COMPAS RPI revealed significant disparities, with black defendants disproportionately classified as high-risk compared to white defendants. Notably, non-recidivating black defendants were nearly twice as likely to be assessed as high-risk, raising concerns about fairness.

This study analyzes Broward County data from ProPublica, including COMPAS scores, two-year recidivism outcomes, and demographic variables, focusing on African American and Caucasian defendants to examine these disparities.

## Methods

This study employs a quantitative approach to analyze fairness in Recidivism Prediction Instruments (RPIs), focusing on error rates and their impact on sentencing outcomes across demographic groups.

### Test Fairness Definition

A risk score is considered fair if it predicts the likelihood of recidivism equally across different groups. This definition aligns with the concept of calibration, where for any given score $S$=$s$, the probability of recidivism should be the same regardless of group membership:

$\mathbb{P}(Y = 1 \mid S = s, R = b) = \mathbb{P}(Y = 1 \mid S = s, R = w)$


- $Y=1$ indicates recidivism
- $S$ is the risk score
- $R$ denotes the demographic group

### Error Rate Analysis

To evaluate fairness, the study analyzes the following error rates by simplifying risk scores into binary outcomes: high-risk (HR) or low-risk (LR) classifications.

- #### Risk Score Coarsening

	The continuous risk score $S(x)$ is transformed into a binary classifier $S_{c}(x)$ based on a threshold $s_{HR}$:

	$S_c(x) = \text{HR}, \text{if } S(x) > s_{\text{HR}} \quad \text{LR}, \text{if } S(x) \leq s_{\text{HR}}$


- #### Key Error Metrics

	- **False Positive Rate (FPR):** The probability of incorrectly classifying a non-recidivist as high-risk.
	- **False Negative Rate (FNR):** The probability of incorrectly classifying a recidivist as low-risk.
	- **Positive Predictive Value (PPV):** The probability that an individual predicted as high-risk actually reoffends.
	- **Prevalence ($p$):** The base rate of recidivism in the population.

- #### Relationship Between FPR, FNR, PPV, and $p$

	$FPR = \frac{p}{1 - p} \cdot \frac{1 - \text{PPV}}{\text{PPV}} \cdot (1 - \text{FNR})$
	
	This equation shows that even when a model is fair in predictive probabilities, differences in recidivism rates ($p$) across demographic groups will lead to unequal FPR and FNR, which can result in disparate impacts.

### Impact Assessment

To quantify the real-world consequences of disparities in error rates, the study models sentencing outcomes using a "MinMax" penalty policy, which applies different penalties based on the risk classification.

- #### MinMax Penalty Policy

	Under the MinMax penalty framework, individuals classified as high-risk receive stricter penalties, while those classified as low-risk receive more lenient penalties. This is formalized as:

	$T_{\text{MinMax}} = t_L, \text{if } S_c = \text{Low-risk}; \quad t_H, \text{if } S_c = \text{High-risk}$

	- $T_{MinMax}$​ represents the penalty assigned based on risk classification
	- $t_L$​ is the penalty for individuals classified as low-risk
	- $t_H$​ is the penalty for individuals classified as high-risk
	- $S_c$​ is the binary risk classification derived from the coarsened score

- #### Corollary Analysis

	- Corollary 3.1 (Non-Recidivators):

		$\Delta = (t_H - t_L) \cdot (\text{FPR}_b - \text{FPR}_w)$


		Higher false positive rates (FPR) for black defendants lead to harsher penalties for innocent individuals, even though they pose no real risk.

	- Corollary 3.2 (Recidivators):

		$\Delta = (t_H - t_L) \cdot (\text{FNR}_w - \text{FNR}_b)$


		Higher false negative rates (FNR) for white defendants result in lenient sentencing for individuals who genuinely pose a risk, while black defendants face stricter penalties.

## Key Findings

1. **Disparate Impacts Exist Even Without Predictive Bias**

	Recidivism Prediction Instruments can still produce disparate impacts between demographic groups, even when they are statistically fair. Even when a model is technically fair, the average penalty difference between groups, such as black and white defendants, can reach up to 24.5% under the same judicial policy.

2. **Impact of High Recidivism Rates**

	When the recidivism rate is high, the false positive rate (FPR) tends to increase, even if the positive predictive value (PPV) remains constant. This explains why groups with higher recidivism rates often experience elevated FPRs, leading to more individuals being incorrectly labeled as high-risk.

3. **The FPR-FNR Imbalance**

	The imbalance between the false positive rate (FPR) and false negative rate (FNR) results in disparate impacts:

	- **Higher FPR:** Non-recidivating individuals are more likely to be incorrectly classified as high-risk, exposing them to unnecessary punitive measures.

	- **Lower FNR:** Actual recidivists are more likely to be correctly identified, but this comes at the cost of harsher judicial scrutiny and potentially more severe consequences for individuals from certain groups.

## Critical Analysis

### Strengths
- **Rigorous Theoretical Framework** 
The paper provides a mathematically rigorous analysis of fairness in Recidivism Prediction Instruments (RPIs), offering formal proofs that highlight inherent trade-offs between fairness metrics.

- **Clarification of Fairness Trade-Offs**
Why fairness trade-offs are inevitable when base rates (recidivism prevalence) differ across groups.

- **Policy-Relevant Insights** 
By linking error rate disparities to real-world consequences under judicial policies, the paper bridges the gap between algorithmic fairness and legal policy.

### Weaknesses

- **Simplistic Treatment of Judicial Decision-Making**
The MinMax penalty policy simplifies the complexity of judicial decision-making, which often involves multiple factors beyond risk scores, such as legal discretion, socioeconomic background, and court biases.

- **Narrow Focus on Binary Classification**
The analysis assumes a binary classification of risk (high-risk vs. low-risk), which may not capture the nuances of continuous risk assessment tools used in real judicial settings.

### Potential Biases

- **Dataset Bias**
Reliance on data from Broward County introduces potential biases rooted in historical policing practices, judicial decision-making, and sampling limitations.

- **Algorithmic Assumptions**
The paper assumes that fairness can be evaluated solely through statistical metrics, potentially overlooking qualitative factors such as societal perceptions of fairness or ethical considerations that cannot be captured by quantitative analysis alone.

### Ethical Considerations

The paper raises critical questions about the ethical use of risk assessment tools in the criminal justice system, particularly when such tools reinforce systemic biases under the guise of statistical fairness.

It highlights the risk of over-reliance on algorithmic decisions without accounting for their disproportionate impacts on minority populations, emphasizing the need for human oversight and policy-level interventions.

---
## [Algorithmic decision making and the cost of fairness](https://arxiv.org/pdf/1701.08230) 

## Introduction and Motivations 
Algorithmic decision making models are increasingly used in the criminal justice system to assess risk and inform sentencing, but their implementation has raised concerns about racial bias and fairness. The paper examines algorithmic decision-making focusing on the COMPAS risk assessment tool, which assigns defendants a risk score (1–10) based on over 100 factors, including age, sex, and criminal history, to help judges decide whether to detain or release defendants before trial. Prior studies have found significant racial disparities in COMPAS scores, with black defendants being more than twice as likely as white defendants to be classified as high-risk despite similar actual reoffense rates. Additionally, COMPAS has been criticized for its higher false positive rate among black defendants, meaning they are more likely to be incorrectly labeled as high risk. This led to some questions about how fairness can be added to algorithms without compromising public safety. In response, researchers have proposed various fairness driven decision algorithms to mitigate racial disparities. The study explores whether such fairness measures can be reconciled with public safety and what trade-offs arise when enforcing fairness constraints.

The main motivation of this paper is to examine fairness through optimization and evaluating whether enforcing fairness constraints leads to a tradeoff with overall decision accuracy and public safety. The authors explore different definitions of fairness and how enforcing them affects crime rates, racial disparities, and decision-making efficiency. 


## Methods

### Defining Measures of Algorithmic Fairness:
- **Statistical Parity**: Equal proportion of defendants are detained in each race group. 
$$E[d(X) \mid g(X)] = E[d(X)]$$
- **Conditional Statistical Parity**: Controlling for a limited set of “legitimate” risk factors, an equal proportion of defendants are detained within each race group.
	- Example: Among defendants who have the same number of prior convictions, black and white defendants are detained at equal rates. $$E[d(X)\mid l(x),g(X)] = E[d(X)\mid l(x)]$$

- **Predictive Equality**: The accuracy of definitions is equal across race groups, as measured by the false positive rate (FPR).
	- Among defendants who would not have gone on to commit a violent crime if released, detention rates are equal across race groups. $$E[d(X)\mid Y=0,g(X)] = E[d(X)\mid Y=0]$$

- **Immediate Utility**: Decision metric that  captures the proximal costs and benefits of a decision rule.
	- Policymakers would prefer to maximize utility as the benefits outweigh the costs.
	$$u(d, c) = E [ d(X)(p_{Y\mid X} - c)]$$  
  This equation reveals that it is beneficial to detain an individual precisely when $p_{Y\mid X} > c$.
    
With the assumptions that:
1. All violent crimes are assumed to be equally costly because Y is binary.
2. The cost of detaining every individual is assumed to be c, regardless of personal characteristics.

### Optimization Decision Rule: 
The paper frames the problem of designing fair algorithms as an optimization problem where the goal is to maximize immediate utility subject to fairness constraints. The theorem provides the form of the optimal decision rules $d$ that maximizes $u(d, c)$ under various fairness conditions.

- The **unconstrained optimum** is to detain individuals if and only if $p_{Y \mid X} \ge c$, where $p_{Y\mid X}$ is the probability that an individual with attributes X will commit a violent crime.

- Under **statistical parity**, the optimum is to detain individuals if and only if $p_{Y \mid X} \ge t_{g(X)}$, where $t_{g(X)}$ is a threshold that depends on group membership. To satisfy **predictive equality** the optimal rule is the same with different values for the group-specific thresholds.

- Under **conditional statistical parity**, the optimum is to detain individuals if and only if $p_{Y \mid X} \ge t_{g(X)l}l(X)$ where $t_{g(X)}l(X)$ represents group membership and legitimate attributes.

In summary, the mathematical theorems in the paper lead to an optimal equation by formally defining fairness criteria, expressing the objective as maximizing immediate utility, and then deriving the optimal decision rules under different fairness constraints using mathematical optimization techniques.


### Empirical Analysis
The study uses data from Broward County, Florida, to investigate the practical implications of the trade-off between fairness and public safety. The data consists of black and white defendants with COMPAS risk scores. A risk assessment model is retrained using L1-regularized logistic regression and Platt scaling to estimate the risk of an individual committing a violent crime if released. They train their model on 70% of the data and evaluate performance on the remaining 30%, repeating this process across 100 random train-test splits. Two key quantities are estimated: (1) the increase in violent crime from releasing more high-risk defendants and (2) the proportion of detained defendants who are actually low-risk.

## Key Findings
1. **Trade-Offs Between Fairness and Public Safety**
    - **The Impossibility Result**: Researchers determined that no algorithm can simultaneously satisfy calibration, balance for negative class, and balance for positive class. 
    - Removing fairness constraints allows for a single optimal decision threshold, maximizing public safety but still leading to racial disparities. 

2. **The Necessity of Race-Specific Decision Thresholds**
    - To meet fairness constraints, such as equal false positive rates, different racial groups must have different decision thresholds. 

3. **Empirical Validation on Real-World Data**
    - In the Broward County dataset, the trade-offs between fairness and crime rates were statistically significant, so this means fairness interventions could not be ignored in real-world applications. 
    - Retrained risk assessment model outperforms COMPAS in terms of AUC (0.75 vs. 0.73), but enforcing fairness constraints leads to unintended consequences.
    - Ensuring fairness results in an increase in violent recidivism while also detaining more low-risk defendants.


## Critical Analysis

### Strengths
- **Mathematical Rigor**
This paper seeks to mathematically define algorithmic fairness and its definitions providing a foundation for comparing and contrasting these different notions of fairness. Developed a theorem that  demonstrates that under certain fairness constraints, the optimal algorithms require applying multiple, race-specific thresholds to individuals’ risk scores. The theorem also shows that the optimal unconstrained algorithm requires applying a single, uniform threshold to all defendants.

- **Real-World Application**
By applying the model to real criminal justice data, the authors bridge the gap between abstract theory and practical implications. This analysis shows that satisfying common fairness definitions can result in detaining low-risk defendants while increasing violent crime rates.

- **Highlights Tension Between Fairness and Public Safety**
Adhering to fairness definitions can decrease public safety, while optimizing for public safety alone can produce stark racial disparities. This paper outlines that different fairness criteria are all necessary in conflict, thus informing better policy decisions. 

### Weaknesses
- **Race-Centric Analysis**
The study primarily focuses on black and white populations, without considering risk scores for other racial groups such as Asians, Mexicans, and Indians.

- **Lack of Factor Analysis**
Does not identify which factors were most accurate or indicative of risk scores, instead placing emphasis mainly on race.

- **Limited Scope**
While the study examines pretrial detention, it generalizes its findings to other areas like lending and hiring, where fairness concerns may differ.

- **Static Decision Making**
The model does not account for long-term effects, such as policy impacts on future crime rates. Additionally, COMPAS only considers binary decisions (hold or release), excluding intermediate options like group supervision.

 ### Ethical Considerations
- **Disparate Impact**
The paper raises an important ethical dilemma. The main question is about if we should allow different racial groups to have different decision thresholds in regards to fairness, even if it conflicts with equal treatment principles. 

- **Policy Implications**
Implementing race-specific thresholds could lead to legal and political challenges, as it might be seen as racial profiling. 


## Conclusion

This paper provides an important contribution by analyzing the tension between fairness constraints and decision-making efficiency. It highlights that no fairness criteria is neutral and every choice impacts either predictive accuracy, fairness across groups, or broader societal outcomes. The findings challenge the naive view of fairness and underscore the need for detailed policy discussions when deploying algorithms in high-stakes settings. 

---

## [Inherent Trade-Offs in the Fair Determination of Risk Scores](https://arxiv.org/pdf/1609.05807) 

## Introduction and Motivations

Risk scoring systems are extensively used in high-stakes domains such as criminal justice, healthcare, and online advertising. These systems produce probability estimates—**risk scores**—that help inform decisions ranging from bail or sentencing to medical diagnosis and targeted advertising. Recent debates have highlighted concerns regarding **algorithmic fairness**, particularly whether these scores treat different demographic groups equitably.

This paper focuses on formalizing three natural fairness conditions that one might want a risk scoring system to satisfy:

1. **Calibration Within Groups**  
   For every group $t$ and for any risk score (or “bin”) $v_b$, the fraction of individuals in that group who are truly positive should equal $v_b$. Mathematically, if a group of individuals is assigned score $v_b$, then:
   $\Pr(\text{positive} \mid \text{score}=v_b,\, \text{group}=t) = v_b$.

2. **Balance for the Negative Class**  
   Among individuals who are truly negative, the **average score** should be the same across groups.

3. **Balance for the Positive Class**  
   Similarly, among the truly positive individuals, the **average score** should be equal across groups.

These conditions ensure that the scores mean the same thing regardless of group membership and that individuals with the same true outcome are treated similarly.


## Methods

The authors formalize the problem using the following components:

- **Feature Vectors**  
  Every individual is described by a feature vector $\sigma$ and an associated true probability $p_\sigma$ of belonging to the positive class.

- **Groups**  
  Individuals belong to one of two groups (for example, based on race or gender). While the distributions over feature vectors may differ between groups, it is assumed that once $\sigma$ is given, the group membership does not affect the true probability $p_\sigma$.

- **Risk Assignment**  
  A risk assignment divides individuals into bins. Each bin $b$ is assigned a score $v_b$. The assignment is represented by a matrix $X$ where $X_{\sigma b}$ indicates the fraction of individuals with feature vector $\sigma$ assigned to bin $b$.

- **Matrix Formulation of Calibration**  
  Let:
  - $n_t$ be the vector counting the number of individuals with each feature vector in group $t$
  - $P$ be a diagonal matrix with entries $P_{\sigma \sigma} = p_\sigma$
  - $V$ be a diagonal matrix of bin scores (with $V_{bb} = v_b$)

  Then, **Calibration Within Groups (A)** can be written as:
  $n_t^\top P X = n_t^\top X V$

- **Balance Conditions**  
  Define $\mu_t = n_t^\top P X \, e$ as the total (expected) number of positives in group $t$ (with $e$ being the vector of ones). Then:

  - **Balance for the Positive Class ( C )**
    $\frac{n_1^\top P X \, v}{\mu_1} = \frac{n_2^\top P X \, v}{\mu_2}$

  - **Balance for the Negative Class (B)**
    $\frac{n_1^\top (I-P)X \, v}{N_1 - \mu_1} = \frac{n_2^\top (I-P)X \, v}{N_2 - \mu_2}$
    where $N_t$ is the total number of individuals in group $t$

These formulas establish the framework for proving the impossibility theorem regarding the coexistence of all three fairness conditions.

## Key Findings

1. **Impossibility Theorem**  
   The central result shows that a risk assignment can satisfy **Calibration (A)**, **Balance for the Negative Class (B)**, and **Balance for the Positive Class ( C )** simultaneously only under one of two conditions:
   - **Perfect Prediction**  
     Every feature vector has a definitive outcome, i.e., $p_\sigma \in \{0,1\}$ for all $\sigma$.
   - **Equal Base Rates**  
     The groups have identical positive rates, i.e.,
     $\frac{\mu_1}{N_1} = \frac{\mu_2}{N_2}$

   In any realistic setting where the base rates differ and predictions are imperfect, **at least one fairness condition must be violated**.

2. **Approximate Fairness**  
   Even if the fairness conditions are relaxed to allow an $\epsilon$-approximation, the data must be nearly perfect or the base rates nearly equal for all conditions to hold approximately. This reinforces the inherent trade-off among fairness measures.

3. **Computational Hardness**  
   For *integral risk assignments* (where all individuals with the same feature vector $\sigma$ are assigned to the same bin), determining whether a non-trivial fair assignment exists is NP-complete. This result implies that finding fair risk assignments is computationally challenging.

4. **Implications for Practice**  
   Designers must make trade-offs among fairness criteria. There is no “free lunch”: if a system enforces calibration and one type of balance, it may have to compromise on the other. This forces decision-makers to prioritize fairness criteria based on the application context.

## Critical Analysis

### Strengths

- **Rigorous Formalization**  
  The paper establishes a clear and precise mathematical framework that defines and relates multiple fairness conditions. This rigor is valuable for both theoretical insights and practical applications.

- **Broad Applicability**  
  The model is general enough to apply across various domains, including criminal justice, healthcare, and advertising, making the results widely relevant.

- **Insightful Trade-Offs**  
  The impossibility result effectively highlights that certain fairness goals are inherently at odds with one another. This insight is crucial for understanding and navigating the challenges of fair algorithm design.

### Weaknesses

- **Assumptions on Data**  
  The analysis assumes that the true probabilities $p_\sigma$ are known and that the feature vector $\sigma$ fully captures an individual’s risk. In practice, these assumptions may be unrealistic, and the presence of estimation errors or unobserved variables can further complicate fairness.

- **Limited Scope of Fairness Criteria**  
  The paper focuses on calibration and balance for the positive and negative classes. Other fairness notions (such as **statistical parity** or **individual fairness**) are not explored, which might be important in some contexts.

### Potential Biases

- **Modeling Bias**  
  By assuming that group membership provides no additional information beyond the feature vector $\sigma$, the model might underestimate sources of bias that arise in real-world data collection and measurement.

- **Simplification of Fairness**  
  While the three criteria are natural, they do not capture the full spectrum of ethical and societal considerations. Factors like long-term impacts and historical inequities are not addressed within this framework.

### Ethical Considerations

- **Policy Implications**  
  The inherent trade-offs suggest that any deployed risk scoring system may disadvantage certain groups in one respect or another. Policymakers must be transparent about these trade-offs and involve stakeholders when determining which fairness criteria to prioritize.

- **Accountability**  
  Recognizing that perfect fairness is unattainable under all metrics raises important questions about responsibility. If a system compromises on one fairness condition, who is accountable for the resulting harm?

- **Ethical Design Beyond Math**  
  While the paper provides a rigorous mathematical treatment of fairness, ethical design must also consider broader social contexts, historical inequities, and the potential for systemic bias. Algorithm designers and decision-makers should take these aspects into account when deploying risk scoring systems.

---
## [On the (im)possibility of fairness](https://arxiv.org/pdf/1609.07236) 

## Introduction and Motivations 

Machine learning algorithms have become deeply integrated into decision-making systems, aiming to replace subjective human decisions with objective algorithmic methods. However, concerns about fairness in these systems have emerged, as research demonstrates that ML models can learn and reproduce discriminatory behaviors in a similar manner as human decision making. The central issue in algorithmic fairness revolves around preventing models from perpetuating bias. This paper seeks to mathematically formalize fairness to expose the underlying value systems embedded in decision-making models. The authors argue that fairness requires explicit assumptions about how these spaces are related to each other. They introduce two views, “What You See Is What You Get” (WYSISYG) and “We’re All Equal” (WAE), and examine how they impact algorithmic fairness. The goal is to allow for a conscious choice of belief systems and to ensure that fairness mechanisms align with these beliefs.

### Key Definitions
- **Nondiscrimination**: The process of decision-making does not vary based on group membership.

- **Group**: A collection of individuals that share a certain set of characteristics (gender, race, religion, etc.).

- **Group Membership**: A characteristic of an individual.

- **Structural Bias**: Unequal treatment of groups.

- **Group Skew**: The way in which a group (geometric) structure might be distorted between spaces.

## Methods
The authors define three key spaces involved in algorithmic decision-making.
1. **Construct Space**:  The space containing the features we would like to make a decision based on (ex: intelligence).
2. **Observed Space**: Consists of measurable features that can be observed (ex: SAT score).
3. **Decision Space** Represents the final decision outputs (ex: college admission decision).

The authors first defined fairness in which a decision process is fair if the individuals close in the construct space receive similar outcomes in the decision space. Fairness aware algorithms are mappings between spaces where inputs are taken from some feature space and return outputs in a decision space. To evaluate fairness, the paper introduces **Gromov-Wasserstein distance** (GWD), a metric that compares transformations between these spaces, helping to quantify distortions in decision outcomes. The GWD computes the Wassertanian distance (WD), the optimal transportation between two sets and computes the resulting distance, between the sets of pairs of points, to determine whether the two point sets determine similar sets of distances. It is defined by the equation: $$GW(X,Y) = \frac{1}{2} inf \int \int \mid d_X(x,x’) -d_Y)y,y’)\mid d \mu_X* d\mu_Xd\mu_{\gamma}*d\mu_{\gamma}$$

The authors explore fairness assumptions, particularly the **What You See Is What You Get (WYSIWYG) worldview**, which assumes that observed features accurately represent construct space features. The paper also examines the worldview of structural bias, which occurs when distortions between groups exceed distortions within groups, leading to unequal treatment. Using these two worldviews, the authors analyzed how fairness mechanisms performed. The two fairness mechanisms compared were:

 - **Individual fairness mechanisms (IFMs):** Ensure that similar individuals in the observed space receive similar outcomes. 
 - **Group fairness mechanisms (GFMs):** Ensure that groups receive statistically similar outcomes to avoid discrimination.

## Key Findings
The study demonstrates that fairness is achievable under strong WYSIWYG assumptions, provided an individual fairness mechanism exists.
- If WYSIWYG holds, fairness can be achieved using individual fairness mechanisms. 
- If WYSIWYG fails, so there is some structural bias, fairness cannot be guaranteed. 
- Only individual fairness mechanisms achieve fairness, and group fairness mechanisms are unfair.

Group fairness mechanisms, designed to equalize decisions across groups, can also introduce new discrimination.

- Under the we’re all equal (WAE) assumption, group fairness mechanisms can ensure non-discrimination by equalizing group-level outcomes. 
- This may come at the cost of individual fairness, potentially treating individuals unfairly within groups. 
- Only group mechanisms achieve non-discrimination and individual fairness mechanisms are discriminatory.

Specifically, when groups are adjusted to receive similar decisions, members of higher-performing groups may receive worse decisions than less-skilled individuals in lower-performing groups. This suggests that enforcing strict group fairness can create unfair outcomes for certain individuals. The paper highlights the fundamental tension between **individual fairness** (treating similar individuals similarly) and **group fairness** (equalizing outcomes between groups), showing that existing fairness approaches inherently rely on assumptions about fairness worldviews. Fairness under WYSIWYG and non-discrimination under WAE need different mechanisms that are conflicting. Thus, this finding highlights that certain notions of fairness are fundamentally incompatible with one another.

## Critical Analysis

### Strengths
- The paper defines fairness in a structured manner, differentiating between construct, observed, and decision spaces, including a distance metric to quantify distortions between decision making spaces.

- Identifies different fairness worldviews (WYSIWYG vs. structural bias) and their implications for fairness guarantees.

- Found that there are different types of fairness and that some notions of fairness are incompatible with each other.

- Proposes a real life example to enhance clarity and understanding.

### Weaknesses
- Assumes that fairness can be mathematically formalized, but in practice, construct spaces are difficult to define and measure.

- Does not provide empirical validation or case studies, making it difficult to assess the practical implications of the proposed fairness measures.

- The findings highlight that fairness cannot be universally defined as different worldviews contradict, and researchers must be very explicit about their assumptions when designing these systems.

- This paper explores fairness as a mathematical problem rather than considering broader contexts where fairness can be a bit more subjective and oversimplifies perspectives on fairness by categorizing views.

### Ethical Considerations
- Highlights the dilemma of group fairness mechanisms potentially disadvantage other individuals based on the worldview metric applied.

- Assumptions about fairness worldviews may reflect biases in society.

- Policymakers should carefully choose fairness definitions that align with ethical and legal standards rather than simply looking at the mathematics.

## Conclusion

This paper provides a theoretical exploration of fairness in machine learning, demonstrating that fairness definitions depend on underlying assumptions about decision making features and group structures. It highlights the trade-offs between different fairness approaches, showing that ensuring fairness for one group may inadvertently introduce new biases. While the framework is mathematically proved, its real world applicability remains an open question, emphasizing the need for empirical studies to validate its findings.

---
