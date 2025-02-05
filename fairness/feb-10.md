# Fairness - Intro & Bias Sources 

The core theme behind the four papers discussed here is an exploration of how big data and algorithmic systems can perpetuate discrimination, challenging the idea that these systems are objective. We will explore these ideas through the lens of fairness, techological limitations, jurisprudence, and societal impacts.  

## [Fairness and Machine Learning, Ch 1](https://fairmlbook.org/introduction.html). S. Barocas, M. Hardt, A. Narayanan, 2023

### Introduction

Historically, we have used statistics to help us in decision-making, to more accurately predict outcomes. Machine learning builds upon the idea of using statistical measures to help us make decisions, but instead of manually selecting features and calibrating weights by hand,is able to uncover patterns and relationships in data on its own. It has its own flaws, however. To have a good model, you need good data—because a model generalizes outputs based off of its inputs.If data reflects prejudices based on stereotypes or inequalities, the model will also reflect them. The model may also reflect errors in human judgement—for example, younger defendants are statistically more likely to re-offend, but judges are more likely to be less harsh when deciding on their sentences due to the belief that they deserve another chance since they are young


### Demographic Disparities 

Bias due to race is not new in data-driven systems. For example, Amazon uses such a system to decide where they can complete free same-day deliveries—however, neighborhoods that qualified for this perk were twice as likely to be home to white residents than black residents. Even though Amazon says that the decision was driven by efficiency and costs, and not race, this racial disparity could be due to historical inequalities and segregation.

Going forward, how do we define bias in model decisions?

- Bias: demographic disparities in algorithmic systems that are objectionable for societal reasons. 
- Statistical Bias: when expected or average values differ from the true values it aims to estimate. 

Both biases should be considered when developing machine learning models. 


### Machine Learning Loop

How do disparities propagate themselves through the machine learning model process? 

First, measurements are collected, which the model will be trained on. Issues in these values—such as patterns of stereotypes or disproportional representation—can later affect a model trained on the data. Then, a model goes through a learning stage, where we train it on the collected measurements. Afterwards, a model is able to predict outputs. These outputs will be representative of the general patterns learned from the original collected data. Some models continue to learn through feedback, potentially from users—although this can be used to unlearn biases, it may also be another way for bias to arise.

![ML Loop](images/feb10/machine-learning-loop.png)
*Figure 1: Machine Learning Loop*


### The State of Society 

Disparities in people due to gender, socioeconomic factors, discrimination, and others reflect themselves in training data, thus later effecting model outcomes.

What are some examples of this? 

- Bureau of Labor Statistics (2017): some job occupations have stark gender imbalances. Machine learning systems that screen for job candidates might learn this gender division, and discriminate because of it. 
- Street Bump: this tool, designed to automatically collect data on potholes using smartphones, reflecting patterns of phone ownerships. This meant that wealthier neighborhoods had better coverage than lower-income ones, or places with majority elderly populations, who were less likely to own smartphones. 
- Kaggle: Automated Essay Scoring datasets can contain biases from human graders for student essays, potentially from linguistic choices that reflect social groups—which is a pattern that models learned when trained on. 


### The Trouble with Measurement 

The problem with measurement is that it requires defining variables of interest. Biases in definitions, categories, and how we quantifiably measure qualitative metrics such as success come into play. Current social norms are reflected in this, and certain variables have to be reduced to a single number. For example; 

- A good employee might be reduced to performance review scores. 
- A succesful student might be reduced to their GPA. 

Measurements also change over time. Racial categories have evolved: in 2008, "multiracial" became an option on forms. Over time, we've developed new gender labels. These measurements are only available in newer datasets, and not older ones. 


### From Data to Models

Models extract stereotypes represented in data as much as they extract knowledge of bigger pictures we want them to learn. Sometimes, removing features such as gender to remove bias is not enough, due to proxies and other feature correlations with gender. Machine learning algorithms generalize based on the majority culture: which causes issues and errors to more likely occur with minority groups. 

![Gender Stereotypes](images/feb10/gender-stereotypes.png)
*Figure 2: Stereotypes within models can reflect in their outcomes*

For example, the figure above shows how a model learned the association between gender and occupations: Turkish has gender neutral pronouns, but automatically determined the doctor to be a "he" while the nurse was deteremiend to be a "she". 


### The Pitfalls of Action 

We have to pay attention to where models are applied: population characteristics change over time, and different populations may have different cultural / social norms. Models need to reflect these changes! Models are also limited to observing correlations, not necessarily causations—and understanding why models make decisions is important. This is not always easy due to the black-box nature of some algorithms. Model predictions can also affect outcomes that will in turn invalidate its own predictions—if a model observes that there is less traffic using a certain path, and recommends it, that path will receive more traffic due to the suggestion, and may end up with more traffic than other routes. 


### Feedback and Feedback Loops 
 
User feedback can be used to refine models. However, feedback can be misinterpreted, and may also contian user prejudices. Feedback can occur in three main ways: 

- *Self-fulfilling prophecies*: this is esentially confirmation bias. When predicting a certain outcome, this results in looking for that particular outcome, validating itself in the process (without looking at other factors). An example of this is a policing system: knowing that crime occurs more often in a certain neighborhood, more police officers will be sent to that location, which will in turn lead to more arrests and reports of crime—leading to an infinite, self-feeding cycle. 

- *Predictions that affect the training set*: due to self-fulfillment, using model predictions to update a model leads to a feedback loop with bias reinforcing existing bias in a model. Models should only be updated by surprising or new outcomes, since refining it with duplicate data will just cause existing bias to be more solidified. 

- *Predictions that affect the phenomenon and society at large*: long-standing prejudices will be reflected in models, which will keep prejudices alive, which will later reinforce prejudices in models. This again leads to a never-ending cycle of prejudice perception. 


### Getting Concrete with a Toy Example 

![toy_example](images/feb10/toy-example.png)
*Figure 3: GPA vs Interview Score*

The paper references a made-up example where a classifier is trained to predict job performance based on college GPA and an interview score, and determines a cutoff for hiring interviewees. Notice how the cutoff favors triangles over squares, even though it does not take into account whether a person was of the triangle or square group to make its prediction. This is an example of how a demographic group may be represented by proxies in the data—even if gender or race was not explicitly considered, performance scores may reflect manager biases, for example. The point is that removing features that we do not want a model to learn patterns for is not enough, due to proxies and other correlations between data fields. 


### Justice Beyond Fair Decision Making 

- Interventions that Target Underlying Inequities: instead of trying to optimize selections and decisions with a model, we should target the reasons why there might be disparities. For example, instead of judging an employee solely on their performance review score, there should also be a focus on building environment, accessibility, etc, to give everyone better opportunities to be on a level playing field.  

- The Harms of Information Systems (search and recommendation algorithms) 
    - Allocative Harms: when a system withholds groups opportunities / resources. 
    - Representational Harms: when a system reinforces subordination of groups along the lines of identity. This receives less attention due to non-immediate harm caused, but they have long-term effects on culture and stereotypes. 


### Limitations & Opportunities 

Completely unbiased measurements may be infeasible, but we still have to try our best to remove bias where we can. Observational data can be insufficient to identify disparity causes, however, due to lack of understanding of models, but this is necessary to intervene and remedy biases. Ensuring fairness makes model decisions more transparent, forcing the articulation of decision goals—but this requires making models explainable, which can be difficult.


### Critical Analysis

The paper was overall vague: which is good as an introductory chapter, but lacked substance. There were a few good examples to illustrate points, but the separate sections seemed to cover the same points a few times, making the content repetitive.


## [Big Data: A Report on Algorithmic Systems, Opportunity, and Civil Rights](https://obamawhitehouse.archives.gov/sites/default/files/microsites/ostp/2016_0504_data_discrimination.pdf). The White House, 2016

### Introduction
Big data creates opportunities for technological innovations that enhance fairness and reduce discrimination. However, there is a risk that biases may become encoded in automated-decision making. The principle of "equal opportunity by design" is essential in developing technological systems to prevent such biases. To explore the challenges and opportunities big data offers for government policymaking, this report examines several case studies. 

### Challenges in Big Data
- *Data inputs to algorithms*: poorly selected data, incomplete data, inaccurate data, outdated data, selection bias, unintentional promotion of historical biases
- *Design of algorithmic systems*: poorly designed systems that do not account for historical biases, services that unintentionally restrict information flow to certain groups, systems that assume correlation implies causation, disproportionate datasets 
- As technology advances, it may become more difficult to explain decision-making processes unless they are designed to ensure accountability

### Big Data and Access to Credit
**Challenge**: Many Americans lack a sufficient and recent credit repayment history, making it difficult for algorithms to generate them a credit score. This in turn affects their ability to secure loans. 

**How Can Big Data Help?**
- Increase the range of data sources used to assess consumer creditworthiness. This can include phone bills, public records, educational backgrounds, social media, etc.
- Develop new tools with alternative algorithms for credit scoring.

**The Challenges of Big Data with Access to Credit**
- Using historical data for credit assessment may reinforce existing disparities in access to credit.
- Increasing the amount of data sources could introduce inaccuracies, making it essential for consumers to have the right to be informed and the ability to dispute any errors. 
- Expanding the amount of data sources also makes creditworthiness assessments more complex, potentially making it more difficult for consumers (especially those with less experience with the credit scoring system) to interpret notices and identify issues. 
- New credit scoring tools and algorithms must be carefully designed and tested to prevent unintentionally acting as proxies for protected characteristics. Poorly implemented algorithms could produce discriminatory harm. 

### Big Data and Employment
**Challenge**: Traditional hiring practices for identifying candidates may exclude qualified individuals. Even with the introduction of algorithmic systems in the hiring process, "like me" bias persists, with individuals tending to hire candidates similar to themselves. 

**How Can Big Data Help?**
- Algorithmic systems could potentially mitigate individual biases and "like me" bias from hiring managers. They can evaluate characteristics and skills that have demonstrated correlation with success at the job. 
- These systems could also help address discrimination challenges such as the wage gap and occupational segregation.

**The Challenges of Big Data with Employment**
- Hiring algorithms that consider protected characteristics, such as race, may not reliably predict job success. Similarly, using creditworthiness and criminal records may not accurately reflect an individual's qualifications. 
- Historical biases in data can be perpetuated by algorithms and lead to discriminatory outcomes. This includes potential age discrimination or education discrimination (disadvantaging individuals without a specific degree or field of study).

### Big Data and Higher Education
**Challenge**: Students often encounter challenges in accessing information about higher education including guidance on choosing the right college and making financial considerations. Staying enrolled and successfully graduating presents further challenges. 

**How Can Big Data Help?**
- *College Scorecard*: a big data tool that provides information on graduation rates, student loan debt, average post-college salaries, and more for different universities. This tool can help students and families make informed decisions about which college best fits their needs or offers the highest return on investment.
- Programs like the Georgia State University Graduation and Progression Success (GPS) Advising Program which tracks 800 risk factors for students such as poor grades, missing prerequisite courses, and finanical struggles. When the risk is detected, the system automatically flags students in trouble and alerts advisors, enabling them to intervene before the student drops out. 

**The Challenges of Big Data with Higher Education**
- *Admission discrimination*: some universities use predictive models to estimate a student's likelihood of graduating before they even enroll. 
    - Denying admission to students from low-income backgrounds because statistical models predict they are less likely to graduate is unfair. 
    - If an admissions algorithm strongly favors students from wealthier neighborhoods due to historically higher graduation rates, it may exclude talented but underprivileged students. 
- *Bias in financial aid decisions*: some universities use data-driven systems to allocate financial aid based on expected student success.
    - If a student's profile suggests they may struggle to graduate, they could receive less financial aid, making it even harder for them to succeed. 
    - This approach reinforces economic inequality rather than addressing it. 
- *Privacy and ethical concerns*: universities colect extensive data on students, yet students have little control over how their information is used. 

### Big Data and Criminal Justice
**Challenge**: Law enforcement officials are looking for new methods to use technology to enhance crime prevention, develop policing strategies, and improve judicial decision making. 

**How Can Big Data Help?**
- Enhance transparency by increasing usage of open policing data which can help foster trust within communities.
- *Predictive policing algorithm*: analyzes past crime data to forecast high-risk locations and times for crime occurrence.
    - The Los Angeles Police Department (LAPD) deployed a predictive policing system that uses historical crime data, weather conditions, and time-based analysis to determine where crimes are most likely to occur. This led to reductions in burglary and auto theft rates as well as more efficient deployment of officers. 
- *Data-driven accountability in law enforcement*: big data systems could be used to track officer behaviors. 
    - The Chicago Police Department (CPD) developed an early warning system that uses data analytics to monitor officers with high rates of civilian complaints, use-of-force incidents, and other misconduct indicators. This led to intervention programs for at-risk officiers, reduction of racial disparities in policing outcomes, and improvement of public trust. Read more [here](https://crimelab.uchicago.edu/projects/officer-support-system-oss/). 

**The Challenges of Big Data with Criminal Justice**
- Predictive policing relies on historical crime data, but if past practices were biased, algorithms can replicate and even amplify those biases.
- Transparency concerns as the public cannot access or challenge the decision-making process in criminal justice cases. Defendents may be unaware of how their risk score was calculate or how to dispute an unfair classification.
- Monitoring social media, tracking mobile phone locations, and analyzing online behavior raise significant privacy and ethical concerns about potential data misuse. 

### Suggestions for the Future
- Support research into mitigating algorithmic discrimination.
- Encourage organizations, institutions, and companies to design transparency and accountability mechanisms in their algorithmic systems. 
- Promote academic research and industry efforts for algorithmic auditing and external fairness testing of big data systems. 
- Increase participation and opportunities in computer science and data science, so more people are informed. 
- Consider the roles of the government and private sectors in the context of big data. 

### Critical Analysis

**Strengths**

This report thoroughly evaluates the challenges and opportunities of using big data in a variety of contexts that relate to government policymaking. Each case study also supports its arguments with concrete examples of existing approaches for more fair usage of big data. Overall, the report also offers suggestions for the future for how we can tackle these big data challenges.

**Weaknesses**

Since this report was released in 2016, there have been significant advances in technological systems, data science, and machine learning. Therefore, the case studies may be missing information that would make it more relevant to our society today. Additionally, although it offers suggestions for the future, there is a lack in detail for specifically how we can achieve those goals.

**Potential Biases**

As a government report, there could be potential biases in this report since it may be presented from a policymaking perspective. In addition, it may highlight the civil rights aspects of these case studies and less of the other benefits of using big data and algorithmic systems such as efficiency. In some cases, there was also less discussion about the positive outcomes of using big data applications for fairness where biases were successfully reduced. 

**Ethical Considerations**

Like the other papers, this work discusses the importance of reducing discrimination and biases while improving fairness to big data applications. There is a huge emphasis about the need to incorporate fairness into the *design* of algorithmic systems through "equal opportunity by design" principles that should be practiced throughout the entire engineering process.


## [Big Data’s Disparate Impact](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2477899). S. Barocas, A. Selbst, 2014

### Introduction and Motivations

While we could trace back human decisions to their source, and hold them directly responsible, can the same be said about an algorithm? If an automated decision is made by an algorithm (say with picking a candidate for a job), who can be held responsible for any discrimination such a decision might have caused?

It is well known that algorithms rely on data - mined from different sources - to make their decisions. Even though efforts can be made to prevent discrimination, when the dataset itself is biased (wanton or not) they tend to propagate to downstream tasks in computer algorithms. This can lead to an unfortunate result of exacerbating already prevalent inequalities which marginalize certain groups. 

The 14th amendment of the US constitution offers the Equal Protection Clause, which led to the passing of the Civil Rights Act of 1964 and its component Title VII - Prohibition of Discrimination in Employment based on race, color, religion, sex, and national origin. This paper explores the idea of fairness and the impact of automated decision making tools through this lens – Title VII can be applied towards remedying some, if not all, of these effects. Since it is backed by law, victims can approach a court to seek redress from discriminatory decisions.

Granted, discriminatory practices are far more widespread and far reaching than employment, the authors of this paper ground their arguments to Title VII given its “particularly well-developed set of case law and scholarship”. They present this as a literature review of academic writing, current events (as of 2014), and case studies of court rulings. While agreeing that the current framework is insufficient to fully tackle the scope of discrimination given the growing use of algorithms, they are motivated by this fact to address the issue. They posit that discrimination can be an artifact of the data mining process itself even without any human intervention. 


### Methods

Over three parts, the authors adopt an interdisciplinary approach, drawing on computer science literature, legal scholarship, and antidiscrimination law.

* The essay first presents an overview of discriminatory mechanisms within the data mining process:
    * Defining target variables and class labels, and how choices in specifying the problem can unintentionally put protected classes at a disadvantage
    * Feature selection within (training) data which can amplify existing biases within the data (“garbage in, garbage out”). They also discuss proxies, where seemingly neutral features can serve to identify membership in protected classes.
* The authors review Title VII jurisprudence, analyzing the disparate treatment & disparate impact theories, and how these doctrines apply to various mechanisms of data mining.
* They also analyze case law and Equal Employment Opportunity Commission (EEOC) guidelines, discussing how courts determine if a practice is justified as a “business necessity” as it relates to data mining.
* They consider both inherent (arising from the mechanisms of data mining) and external (political/legal) difficulties of reforms in ensuring fairness for all.


### Key Findings

* Data mining can lead to discrimination even without intentional bias, since it could be an emergent property of data mining.
* Mechanisms within data mining can lead to discrimination, including how a target variable is defined, how training data is collected and labelled, feature selection, and the use of proxies/masking.
* While data scientists designing algorithms find the greatest risk in false negatives/positives, a greater risk lies in the conceptual accuracy of the class labels, such as the rating an algorithm would give an employee, and the variables considered, such as prior performance reviews.
* Annotating samples is difficult ethically to do by hand while ensuring fairness.
* “Garbage in, garbage out”: as also discussed earlier, algorithms will reflect bias in the data they mine. An example is the LinkedIn talent match feature which recommends candidates to employers based on demonstrated interest in certain candidate properties. This algorithm reflects the social discrimination biases of employers when data mining.
* Privileged people are better documented and have more available data, boosting their rankings in automated job searches
* Under Title VII, an employer can get sued for discrimination under two theories: disparate treatment and disparate impact. Treatment is intentional and impact is from a neutral policy that effectively discriminates. As discriminatory data mining is unintentional it is difficult to argue for treatment. To argue for impact, a plaintiff must find an alternative employment practice that is reasonable and bias-free. Both these tend to be inadequate in their scope while considering data mining.
* Job hiring is inherently subjective so it is difficult to draw a line between discrimination and fair hiring if there is no clear intent to discriminate.
* Reforms in the field face both internal and external challenges, making it difficult to modify anti-discrimination laws to truly benefit protected classes. 


### Critical Analysis

**Strengths**

The essay provides a detailed account of how data mining can lead to discrimination
offers a useful taxonomy of the specific mechanisms within data mining that can generate unfair decisions, and is able to effectively tie CS literature detailing algorithmic bias with real life cases of its impacts on employment discrimination.
The paper details the history of employment discrimination court cases and how they may apply to modern examples of discriminatory data mining when used for job hiring.
They highlight the limitations of current legal frameworks (particularly Title VII) in addressing the challenges of data mining


**Weaknesses**

* While it discusses the limitations of current laws, it offers few specific recommendations for reform.
* As the authors also agree, some, if not most, instances of discriminatory data mining will not generate liability under Title VII.  This is a feature of the current approach to anti-discrimination jurisprudence, which focuses on procedural fairness. 
* The paper is limited to Title VII, and does not fully explore other areas of anti-discrimination law even though it claims the findings apply elsewhere as well. It also limits itself to US law (possibly by design), and could benefit from a discussion of current best practices in other countries.
* Perhaps minor, but the paper includes a lot of jargon which could make it difficult for both sides (technical & legal) to completely understand the ideas presented. Due to the intricate nature of the policies discussed, the paper ends up lengthy and difficult to quickly understand the major points of.

**Potential Biases**

As this paper is structured as a literature review, the selection of literature, court cases, and events discussed could potentially introduce bias. Given that the paper is almost a decade old, the emergence of more equitable practices in the past few years could render some of the arguments invalid.

**Ethical Considerations**

Similar to the first paper, this paper brings up points about where discrimination occurs in models and data, while discussing existing laws, legal topics, concerning data—explains their insufficiency. 



## [Semantics derived automatically from language corpora contain human-like biases](https://www.science.org/doi/10.1126/science.aal4230). A. Caliskan, J.J. Bryson, A. Narayanan, 2017

### Introduction and Motivations 

This paper studies how machine learning models trained on (large) language corpora learn and reflect inherent human biases. This was motivated by the idea that existing text corpora capture cultural and historical biases. They utilize word embeddings to empirically study propagation of these biases to models trained on that corpora. 

Existing works have observed that models learn racial stereotypes based on names. Furthermore, female names are more associated with family than career words, compared to male names. These works have found that other, more general human biases can be observed: for example, flowers have higher correlations with being pleasant, while the word insects is more closely tied to the word unpleasant. Using GloVe word embeddings, the researchers demonstrate that models also capture stereotypes related to gender, regarding occupation and names. 

This work is especially relevant in the light of the increasing use of large language models that are being trained on vast amounts of data sourced from multiple repositories.


### Methods

As mentioned earlier, the researchers primarily use word embeddings, which represent words as vectors in a vector space. Specifically, they use the GloVe (Global Vectors for word representation) embeddings from the “Common Crawl” corpus of the Internet (~840 billion tokens) for this, allowing them to capture semantic relationships and amplify signals better.

* The authors develop the Word-Embedding Association Test (WEAT), which is a statistical test analogous to the Implicit Association Test (IAT). 
* WEAT compares the vectors of word embeddings for the same set of words used by the IAT. It uses a distance measure (specifically cosine similarity) as analogous to reaction time in the IAT.
* Assuming a null hypothesis of no difference between the two sets of target words in terms of their relative similarity, the authors use a permutation test which measures the “(un)likelihood” of the null hypothesis. It computes the probability that a random permutation of the attribute words would produce at least the observed difference in means.
* They also develop the Word-Embedding Factual Association Test (WEFAT) to examine how the embeddings capture empirical information about the world embedded in the corpora.
* They used linear regression analysis to test the association between the normalized association scores and the real-world property.


### Key Findings

![Gender_Association_Figures](images/feb10/gender-association.png)
*Figure 4: Results of the gender correlation study*

* The study successfully replicated a large range of known human biases as measured by the IAT, indicating that biases can be transmitted through language.
* The results replicate the finding that humans find flowers more pleasant than insects, and musical instruments are more pleasant than weapons (!)
* With some data editing, they also replicated the finding that the biases propagate through names - candidates with European-American names get offered more interviews than, say, African American candidates. Also, female names were more associated with family (or arts) than career (or STEM), compared with male names.
* Perhaps more interestingly, the findings can aid a debate on the Sapir-Whorf hypothesis which says that a person’s language influences how they think. This is because the work suggests that behavior can be driven by cultural history embedded within a term.


### Critical Analysis

**Strengths**

* The large size of the dataset (Common Crawl corpus) GloVe embeddings helps support the validity of the findings of the paper.
* IAT is a well established method in the field of psychology, and modelling the WEAT & WEFAT on this strengthens the empirical analysis. The approach differs from the traditional method since the subjects are words, and not people.
* The paper replicates many well-known human biases spanning race, gender, occupations, and age, along with pleasantness associations.
* The null hypothesis and the subsequent statistical analysis provides a compelling explanation of the transmission of biases through language.

**Weaknesses**

* While based on a large corpora, the comparison is mostly text based, and does not include other modalities (like visual). Additionally, published text can be polished, but non-verbal cues also play a critical role in conveying emotions.
* It can benefit from a study of deeper causal association between the words, especially as they appear in other languages. While the authors briefly mention biases implied during statistical machine translations, a detailed study would be beneficial.
* Some low frequency words which could potentially refute the findings were deleted from the corpora.

**Potential Biases**

* As mentioned earlier, the text is from human-generated content from the internet, and misses capturing non-verbal cues (or visual aids), and other conventions which are implied from tone.
* As the authors also acknowledge, the analysis is based on English language text, and other languages are not considered.

**Ethical Considerations**

The paper helps in showing how biases in text propagate to language models, which can help in identifying possible discrimination. As such, it highlights the ethical imperative to deploy systems that are fair by accounting for these inequalities.
