# Introduction

## JailBreak Attacks

Jailbreak attacks are techniques used to bypass the built-in safety mechanisms of AI models, allowing them to generate restricted or harmful content.While there has been some success at circumventing these measures—so-called “jailbreaks” against LLMs—these attacks have required significant human ingenuity and are brittle in practice. Attempts at automatic adversarial prompt generation have also achieved limited success.
Under normal circumstances, LLMs are modelled and aligned to avoid generating objectionable contents. LLM serving as a chatbot would not see this input alone, but embedded in a larger prompt in combination with a system prompt and additional scaffolding to frame the response within the chat framework. Some research works have been succesful in breaking through this, by adding a suffix that the attack will optimize to generate an answer to the original query.

The basic design Elements of a jail break prompt includes:

1. Producing Affirmative Responses. Making sure we get a response from the model after a query that is censored under normal circumstances is important.
2. Formalizing the adversarial objective
3. Greedy Coordinate Gradient-based Search

Things get more interesting in case of vision-integrated LLMs. Continuous and high-dimensional nature of the visual input makes it a weak link against adversarial attacks, representing an expanded attack surface of vision-integrated LLMs. The authors of this paper [46] argue that it should be treated as a security problem which warrants the adaptation of security-based approaches. There are theoretical and fundamental limitations to this approach and semantic censorship can be perceived as an undecidable problem

## Censorship

LLMs blind adherence to provided instructions has led to concerns regarding risks of malicious use. Commonly employed censorship approaches treat the issue as a machine learning problem and rely on another LM to detect undesirable content in LLM outputs. Many existing censorship approaches impose semantic constraints on model output, and rely on another LLM to detect semantically impermissible strings. For example, Markov et al. deemed impermissible strings to be those which contain content pertaining to one of multiple sensitive subjects including sexual content, violence, or self-harm. Paper [46] shows that such semantic censorship suffers from inherent limitations that in the worst case make it impossible to detect impermissible strings as desired

## Types of Jailbreak Attacks

Jailbreak attacks can be divided into two broad categories based on modalities: Textual and Multimodal attacks.

### Textual Attacks

Textual attacks manipulate the input text to bypass the safety mechanisms of large language models (LLMs) and provoke harmful or restricted responses. These attacks exploit the model's language understanding and generation abilities without altering its internal structure.

#### Automated adversarial suffix [46]

This attack involves appending an adversarial suffix to a potentially harmful user query, aiming to trigger negative behavior. The original user query remains unchanged, but extra tokens are added to influence the model's response in a detrimental way. Rather than relying on manual engineering, this method uses a combination of greedy and gradient-based optimization to automatically generate these suffixes. The approach is universal because it finds a single suffix that works across many different prompts, and it is transferable because the same suffix can elicit undesired responses from multiple different models, including black-box systems like GPT-3.5 and GPT-4.

<img src='./mar31/suffix_attack.png' width=400>

The image above is compilation of Screenshots of harmful content generation from ChatGPT (top left), Claude 2 (top right), Bard (bottom left), LLaMA-2 (bottom right).

#### Mosaic prompt attack [47]

The Mosaic Prompt attack is used used to circumvent censorship in large language models (LLMs) by breaking down an impermissible output into smaller, permissible components. Rather than requesting a prohibited result directly, the attacker queries the LLM multiple times with individually harmless prompts that, when combined externally, reconstruct the impermissible content. This method exploits the principle of compositionality, where the meaning of a complex expression is derived from its structure and the semantics of its parts.

<img src='./mar31/mosaic_prompt_attack.png' width=400>

As shown in the above figure, a malicious user could request individual functions that are essential components of ransomware, but each function by itself is benign and allowed. By assembling these components, and assuming they know how to do so, the user could construct ransomware.

#### Encryption based attack [47]

Encryption-based attack users leverage cryptographic principles such as stream ciphers or one-time pad encryption, to bypass output censorship in LLMs. In this approach, a user and the model establish a shared secret key (for example, via the Diffie-Hellman protocol or through training data poisoning), and the model is instructed to produce encrypted outputs. These outputs, although appearing innocuous or permissible to a censorship mechanism, can later be decrypted by the user to recover impermissible content. The key characteristics of this attack include its reliance on the model's instruction-following capabilities, the theoretical security of the encryption used, and the model’s potential memorization of the key.

<img src='./mar31/encryption_attack.png' width=400>

The above image shows that malicious users can provide an LLM augmented with code interpreters with functions specifying how to decrypt the input and encrypt the output.

#### Jailbreak prompt [48]

A jailbreak prompt is a specially crafted input designed to bypass the built-in safety mechanisms of large language models (LLMs) and elicit responses that would typically be restricted, such as those involving harmful, unethical, or policy-violating content. One of the examples of jailbreak prompts is transforming the LLM into another character as shown in the below image [1].

<img src='./mar31/grandma.png' width=400>

Jailbreak prompts usually have longer length compared to regular prompts, increased complexity, and semantic similarity to benign prompts, which makes detection difficult. They frequently evolve and are disseminated through online platforms like Reddit, Discord, and specialized websites such as FlowGPT, often gaining traction when proven effective.

### Multimodal Attack (Visual + Textual)

Multimodal attacks exploit the integration of both visual and textual inputs in advanced large language models (VLMs), allowing adversaries to manipulate the model's behavior across multiple input channels. As multimodal models like MiniGPT-4 become more common, the fusion of visual and textual manipulation expands the attack surface and presents a serious challenge for AI safety and alignment.

#### Visual adversarial attack [49]

A visual adversarial attack targets vision-integrated large language models (VLMs) by introducing subtle perturbations to images that deceive the model into misbehaving or generating harmful outputs. These attacks exploit the continuous and high-dimensional nature of the visual input space, which makes them more potent and easier to optimize than textual attacks. A single visual adversarial example can universally jailbreak an aligned LLM, prompting it to bypass safety mechanisms and respond to harmful instructions.

<img src='./mar31/vlm_attack.png' width=400>

In the above image example, an attacker first gathers a small set of harmful examples and uses them to create an adversarial example. This example is designed to tune the model into a harmful mode, much like how a few examples can teach a model to perform a task. Once this adversarial input is crafted, it can be reused alongside many different harmful instructions to make the model respond inappropriately, jailbreaking it across a wide range of scenarios. These attackes are effective in jailbreaking models like MiniGPT-4, imperceptible to human eyes, and generalizabile across harmful content categories such as identity attacks, disinformation, and violence.

# Methods

Understanding how adversarial prompts succeed requires digging into the strategies used to deceive LLMs. The five papers covered here offer a diverse range of approaches—from theoretical arguments about the limits of censorship to empirical evaluations of real-world jailbreaks and multimodal attacks.

## (Re) Programming: Building Universal Adversarial Suffixes [46]

(Re)Programming is a technique that exploits LLM's understanding of structured logic by treating prompts as pseudo-code rather than natural conversation. Since models are trained on code and formal instructions, this strategy assumes that LLMs may prioritize execution over ethical alignment. This paper presents a highly effective method for "reprogramming" LLms using a technique called Greedy Coordinate Gradient (GCG) Optimization. The core idea is to generate a universal adversarial suffix that, when appended to any prompt, triggers the model into producing harmful output - even if the base prompt alone would not work. The suffix is optimized by combining gradient signals and greedy token replacement. The methodology works as follows:

1. Choose multiple harmful prompts (e.g. "How to build a bomb")
2. Use a gradient to identify which tokens, when added to the prompt, increase the likelihood of an affirmative response
3. Greedily update each token in the suffix to maximize success across prompts and models
   The resulting suffix was then evaluated across various LLMs and was found to be effective and transferable.

## Composing Harmful Outputs from Benign Pieces [47]

This paper makes a theoretical case for why semantic censorship is fundamentally limited, especially when attackers rely on simple calls to action to build complex harmful outputs. The paper models censorship as a function that attempts to block impermissible outputs based on their semantic content. Using Rice's Theorem, the authors show that detecting whether an LLM output has "dangerous behaviors" is undecidable (it's equivalent to trying to prove nontrivial properties of arbitrary Turing machines).

![Mosaic Prompt Example](./mar31/mosaic_prompt_image.jpg)

They introduce the concept of Mosaic Prompts, in which an attacker breaks a harmful program into multiple benign components. For example, the attacker might ask the LLM to output:

- A function to encrypt files
- A function to send files over a network
- A script to delete logs
  These requests are harmless individually, but when combined they become malicious. The methodology doesn't rely on a single exploit, but on a strategic composition of safe-seeming requests.

## Mining and Testing Real-World Jailbreak Prompts [48]

![JAILBREAKHUB Framework](./mar31/jailbreakhub_framework.jpg)

This paper introduces the JAILBREAKHUB framework, a pipeline that collects and analyzes 1,405 jailbreak prompts found in the wild - sources like Reddit, Discord, FlowGPT, and more. They tracked trends, identifying 131 communities and users who consistently refine and share jailbreaks. The prompts were categorized by strategies such as prompt injection, role-play instructions, and obfuscation through spacing and punctuation. They then generated 107,250 forbidden queries (across 13 harmful categories) and tested these prompts on 6 LLMs. For each prompt-model combination, Attack Success Rate (ASR) was measured.

## Jailbreaking with Adversarial Images in Vision-Language Models [49]

This paper is the first to show that adversarial images, not just text, can be used to jailbreak vision-language models (VLMs) like MiniGPT-4, InstructBLIP, and LLaVA. The authors optimize a single image using a gradient-based method, targeting the model's visual input space. They design the image so that when it is paired with harmful textual instruction, the model ignores safety alignment and generates harmful content. This image is optimized using a small toxic corpus of only 66 derogatory prompts, but generalizes far beyond that during inference.

## Generating Diverse Adversarial Behaviors with GCG [50]

This paper provides a broad survey and taxonomy of attack types, but it also demonstrates how to systematically generate adversarial prompts that trigger everything from jailbreaks to information leaks and denial-of-service behaviors.

The authors use Greedy Coordinate Gradient (GCG) optimization to craft adversarial prompts targeting:

- Jailbreak (bypassing alignment)
- Misdirection (redirecting output to malicious URLs)
- Extraction (leaking system prompts)
- Denial of Service (inducing infinite or excessive token generation)
- Role manipulation (hijacking personas or prompt structure)

Prompts are optimized under various constraints—like using only ASCII, emojis, or non-alphabetic tokens—to simulate real-world attack limitations. They run extensive evaluations on LLaMA-2 7B-chat, showing that the attacks succeed even when constrained to weird or malformed inputs. This paper stands out for showing how broad and flexible adversarial attacks can be, and how easily models can be coerced into behaviors far outside their intended function.

# Results

## The GCG (Greedy Coordinate Gradient) optimization method

The GCG (Greedy Coordinate Gradient) optimization method achieves high attack success rates across various large language models (LLMs), including OpenAI's models (ChatGPT - GPT-3.5 and GPT-4) and open-source models like LLaMA-2-Chat, Pythia, and Falcon. The highest attack success rates were observed with the GCG Ensemble method, achieving 86.6% success on GPT-3.5 and 46.9% on GPT-4, as demonstrated in the figure showing "Attack Success Rate (%)" under different settings: Prompt Only, "Sure, here's", GCG (Ours), and GCG Ensemble (Ours). This figure compares the effectiveness of various attack strategies, with the GCG Ensemble approach significantly outperforming previous optimization methods like PEZ and AutoPrompt. Moreover, the adversarial suffixes exhibit strong transferability across different models, particularly those derived from GPT-based architectures. For example, adversarial prompts optimized for Vicuna & Guanacos models successfully transferred to other architectures, indicating the robustness of the proposed attack method. The benchmarking results include various forbidden scenarios such as Illegal Activity, Political Lobbying, Financial Advice, etc., where attack success rates remain consistently high. This demonstrates that the GCG Ensemble method not only improves attack performance but also enhances generalization across diverse models and tasks. The study highlights the urgent need for developing more robust defense mechanisms to address these highly effective adversarial attacks.

<img src='./mar31/Attack_Success_Rate_under_different_settings.png' alt='Performance of different optimizers on eliciting individual harmful strings from Vicuna- 7B.' width='400'>

## Mosaic Prompts

The results of the study demonstrate that current semantic censorship mechanisms for LLMs are inherently limited by their instruction-following capabilities and the possibility of exploiting string transformation techniques. These limitations are evident in scenarios where permissible outputs can be combined to reconstruct impermissible content, making censorship ineffective without severely restricting the model’s utility. The findings suggest that treating censorship as a machine learning problem is fundamentally flawed, and a security-based approach is necessary to address the associated risks effectively.

## Jailbreak Prompts

The experimental results of the study reveal significant findings concerning the efficacy of jailbreak prompts across various platforms and LLMs. The shift from Discord and Reddit to prompt-aggregation websites like FlowGPT as the predominant sharing platforms is evident starting from September 2023, as illustrated in Figure a. Furthermore, while the majority of jailbreak prompts are shared by amateurs, a minority of persistent users (28 accounts) have actively refined and shared jailbreak prompts over long periods, averaging nine prompts each across 100 days (Figure b). Notably, the most common targets of these attacks are ChatGPT (GPT-3.5) and GPT-4, constituting 89.971% and 2.655% of all targets, respectively (Figure c). Moreover, the length of jailbreak prompts significantly exceeds regular prompts, with an average token count of 555 compared to regular prompts' average of 370 (Figure d). Our evaluation of 11 jailbreak communities shows diverse strategies, with the most effective prompts achieving attack success rates (ASR) of up to 1.000 on GPT-3.5 and GPT-4, especially against scenarios such as Political Lobbying, Legal Opinion, and Pornography (Table).

<img src='./mar31/48_Firgure_3.png' alt='Statistics of regular prompts and jailbreak prompts' width='400'>

<img src='./mar31/48_Table_4.png' alt='Results of jailbreak prompts on different LLMs' width='400'>

## Visual Adversarial Examples

The experimental results demonstrate that the proposed adversarial attack method effectively increases the susceptibility of the targeted models to harmful instructions across multiple categories, including identity attacks, disinformation, violence/crime, and general malevolence (X-risk). The visual adversarial examples exhibit significant increases in the model’s propensity to generate harmful content compared to the baseline models without adversarial inputs. Notably, the visual adversarial examples are shown to be more effective than text-based attacks due to the continuity and high dimensionality of the visual input space. This effectiveness is particularly evident when comparing optimization loss between visual and text attacks as illustrated in Figure.

<img src='./mar31/49_Figure_3.png' alt='Comparing the optimization loss (of Eqn 1) be- tween the visual attack and the text attack counterpart on MiniGPT-4. We limit adversarial texts to 32 tokens, equiva- lent to the length of image tokens.' width='400'>

Furthermore, the adversarial attack demonstrates transferability across models, as summarized in Table, where attacks optimized on a surrogate model successfully transfer to other models like MiniGPT-4, InstructBLIP, and LLaVA​.

<img src='./mar31/49_Table_3.png' alt='Transferability of Our attacks.' width='400'>

# Critical Analysis

The reviewed papers collectively highlight the persistent vulnerability of LLMs to adversarial attacks despite various alignment techniques such as RLHF, fine-tuning, and external safeguards. A critical issue is the over-reliance on machine learning-based alignment approaches, which are often circumvented by well-crafted prompts or adversarial inputs.

The work by Zou et al. (2023) provides strong evidence of transferability in adversarial prompts, suggesting that training models on diverse datasets alone is insufficient for ensuring robustness. Meanwhile, the paper by Glukhov et al. (2023) emphasizes the theoretical limitations of semantic censorship, correctly arguing that alignment should be addressed as a security problem. This perspective is further supported by Geiping et al. (2024), who provide examples of various coercion techniques that extend beyond simple jailbreaks.

Moreover, the integration of visual inputs into LLMs, as explored by Qi et al. (2023), introduces additional complexity. The continuous nature of visual data makes it an attractive attack vector, challenging current defensive measures designed primarily for textual inputs. Shen et al. (2024) further demonstrate how prompt-sharing communities evolve over time to circumvent even the latest safeguards.

However, the papers have limitations. While they provide evidence of vulnerabilities, they do not propose comprehensive solutions to mitigate the underlying issues. Additionally, the theoretical argument by Glukhov et al. (2023) that censorship is an undecidable problem, while intellectually compelling, lacks practical evidence demonstrating its direct implications.

# Conclusion

Based on the five papers reviewed, the common conclusion is that adversarial attacks against large language models (LLMs) remain a significant and evolving threat. Despite various attempts at alignment and censorship, including model fine-tuning, reinforcement learning from human feedback (RLHF), and external moderation tools, LLMs are still vulnerable to maliciously crafted inputs. These adversarial techniques range from automatic prompt generation to jailbreak prompts, visual adversarial examples, and various coercion strategies that exploit LLM weaknesses. The persistence of these vulnerabilities highlights a fundamental challenge in AI alignment and safety, particularly as models grow in complexity and are integrated into multimodal systems. Addressing these security concerns requires rethinking alignment strategies and treating them as both a machine learning and a computer security problem, emphasizing the need for robust defenses that can adapt to the continuously evolving attack landscape​.

# References

[46]. Universal and Transferable Adversarial Attacks on Aligned Language Models. A. Zou, Z. Wang, N. Carlini, M. Nasr, J. Z. Kolter, M. Fredrikson, 2023.

[47]. LLM Censorship: A Machine Learning Challenge or a Computer Security Problem?. D. Glukhov, I. Shumailov, Y. Gal, N. Papernot, V. Papyan, 2023.

[48]. “Do Anything Now”: Characterizing and Evaluating In-The-Wild Jailbreak Prompts on LLMs. X. Shen, Z. Chen, M. Backes, Y. Shen, Y. Zhang, 2023.

[49]. Visual Adversarial Examples Jailbreak Aligned Large Language Models. X. Qi, K. Huang, A. Panda, P. Henderson, M. Wang, P. Mittal, 2023.

[50]. Mesmerizing the Machine: Coercing LLMs to do and reveal (almost) anything. J. Geiping, A. Stein, M. Shu, K. Saifullah, Y. Wen, T. Goldstein, 2024.
