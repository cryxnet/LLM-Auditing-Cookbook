A overview about the OWASP Top 10 for Large Language Model (LLM)
## Overview
 
![[assets/OWASP-Top-10-for-LLM-Applications-Artifacts_v1.1_Original.webp]]

### **LLM01: Prompt Injection**

Prompt injection is when someone gives a Large Language Model (LLM) specially crafted input to make it behave in ways that weren’t intended, potentially leading to unauthorized actions or leaking sensitive information. This works because LLMs follow patterns in text without truly understanding the context or the difference between good or bad actions. Instead of fixing a bug in the software, attackers exploit how LLMs are designed to work with text.

**How it works:**
LLMs generate responses by predicting the next word or phrase based on the input they receive. They don't inherently know the difference between a safe command and a dangerous one—they just follow the patterns they’ve been trained on. When someone crafts a prompt that gives conflicting or misleading instructions, the model follows along without recognizing it’s doing something wrong.

There are two main types of prompt injections:
1. **Direct Prompt Injection**: An attacker provides a prompt directly to the LLM that bypasses its safety mechanisms. For example, attackers might use a method like "Do Anything Now" (DAN), which instructs the LLM to ignore the rules or safety limits put in place. The LLM follows these instructions because it’s trained to respond to whatever it’s told, even if it’s something that breaks its intended functionality.

2. **Indirect Prompt Injection**: Here, the harmful prompt is hidden in data that the LLM uses, rather than being directly given by the user. For instance, if an LLM summarizes reviews from the internet, a malicious actor could hide a prompt in the text that the LLM will interpret as an instruction. Since the LLM can’t tell if this hidden text is part of the input or an actual instruction, it may perform actions it wasn’t supposed to, like running unauthorized code or giving incorrect advice.

---

### **LLM02: Insecure Output Handling**

Insecure output handling occurs when an LLM's generated text is accepted and used by another system without proper checks or safeguards. This can lead to serious issues like cross-site scripting (XSS) or remote code execution, where attackers can run malicious code on the system using the LLM.

**How it works:**
LLMs can generate text that looks like code or commands, and if this text is sent to another system without validation (to check if it’s safe), that system might execute it as real code. For example, if an LLM is used to summarize reviews, and one of the reviews contains a hidden JavaScript command, the LLM might output this command in its summary. If a web browser interprets this as real code, it could allow the attacker to control parts of the website.

---

### **LLM03: Training Data Poisoning**

Training data poisoning happens when someone intentionally manipulates the data used to train or fine-tune an LLM, which can introduce hidden vulnerabilities or biases into the model. Since LLMs are trained on massive amounts of data, it’s difficult to vet all of it, making this a tough issue to prevent.

**How it works:**
LLMs learn patterns from the data they are trained on. If an attacker introduces bad data into the training set, it can cause the model to behave incorrectly or unethically. For example, if poisoned data teaches the LLM to favor certain biased outputs, it could skew the model's predictions, leading to harmful or unreliable responses.

---

### **LLM04: Model Denial of Service (DoS)**

Model denial of service (DoS) happens when an attacker overloads an LLM with prompts that use up too many resources, causing the system to slow down or crash, making it unavailable for normal use.

**How it works:**
LLMs consume a lot of computational power to process and generate responses. If someone sends too many requests, overly complex prompts, or makes the model enter a recursive loop (where the output is fed back into itself), it can overwhelm the system. This uses up server resources, making the model slow or unavailable to other users, similar to how a traditional DoS attack works on websites.

---

### **LLM05: Supply Chain Vulnerabilities**

Supply chain vulnerabilities come from third-party components such as plugins, pre-trained models, or external data used by the LLM system. If these external sources are compromised, they can introduce vulnerabilities into the LLM, even if the core model is secure.

**How it works:**
An LLM relies on third-party libraries, pretrained models, or external data sources. If any of these components are compromised by an attacker, the LLM can inherit the vulnerability. For example, if a third-party plugin used with the LLM has a security flaw, an attacker could exploit this to inject harmful data or take control of the system. These vulnerabilities are harder to detect because they come from outside the LLM itself.

---

### **LLM06: Sensitive Information Disclosure**

Sensitive information disclosure occurs when an LLM inadvertently reveals private or confidential data, either because it was improperly trained on sensitive data or because the prompt encourages it to generate such information.

**How it works:**
LLMs are trained on large datasets, which can sometimes include sensitive information if that data wasn’t properly cleaned. If a user asks the right question, the model might reveal proprietary or confidential data it has been exposed to during training. Additionally, user prompts and interactions may be logged and used as training data, which could unintentionally leak private information from previous interactions.

---

### **LLM07: Insecure Plugins**

Insecure plugins refer to vulnerabilities in plugins specifically developed for the LLM system, rather than third-party components. These plugins might allow unsafe actions by not validating or sanitizing the LLM's outputs, leading to dangerous outcomes like remote code execution.

**How it works:**
Plugins can extend an LLM’s functionality, but if they accept unfiltered text or commands from the LLM without checking them, attackers can exploit this to run malicious actions. For example, an insecure plugin might accept a prompt from the LLM that causes it to execute system commands, leading to remote code execution or data breaches.

---

### **LLM08: Excessive Agency**

Excessive agency occurs when an LLM is given too much access, permission, or control over systems or data. This can lead to unintended consequences, such as unauthorized file access, deletion, or modification.

**How it works:**
LLMs might interface with other systems, like reading or writing files. If an LLM has more permissions than necessary (like the ability to write or delete files when it only needs to read them), it can accidentally or maliciously alter or delete important data. Excessive agency occurs when the LLM is given more power than it should have, which opens up opportunities for misuse or errors.

---

### **LLM09: Overreliance**

Overreliance happens when users trust the outputs of an LLM without verifying them, assuming the model is always correct. This can lead to poor decisions, especially if the LLM generates inaccurate or fabricated information.

**How it works:**
LLMs are not perfect and can sometimes generate incorrect or misleading information. If users take the model’s responses at face value without checking them, they may make decisions based on faulty data. For example, an LLM might generate a legal summary that seems correct but is actually inaccurate, leading to poor business or legal decisions.

---

### **LLM10: Model Theft**

Model theft occurs when attackers gain access to an LLM’s internal structure, training data, or algorithms, either by exploiting system vulnerabilities or by reverse-engineering the model based on its outputs.

**How it works:**
LLMs contain proprietary data and algorithms, and attackers may try to steal these to build their own models or sell the information. This can happen through direct hacking of the model’s repository or by carefully analyzing the LLM’s outputs to recreate its underlying system (reverse engineering). Once stolen, the model can be used for unethical purposes or resold, damaging the original creators’ business.


| Risk                             | Description                                                             | Example                                                            | How to Prevent                                                           |
| -------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| Prompt Injection                 | Malicious inputs causing unintended outputs.                            | A disguised command in a chatbot revealing sensitive info.         | Input validation, strict input guidelines, context-aware filtering.      |
| Insecure Output Handling         | Failing to sanitize or validate outputs, leading to attacks.            | An LLM-generated script causing an XSS attack.                     | Sanitize outputs, encode and escape outputs.                             |
| Training Data Poisoning          | Manipulation of training data to skew model behavior.                   | Biased data causing a financial LLM to recommend poor investments. | Validate and clean data, detect anomalies.                               |
| Model Denial of Service          | Overwhelming the LLM with requests causing slowdowns or unavailability. | Resource-intensive queries overloading the system.                 | Rate limiting, monitor queues, optimize performance, scaling strategies. |
| Supply Chain Vulnerabilities     | Compromised third-party services or resources affecting the model.      | Tampered data from a third-party provider manipulating outputs.    | Security audits, monitor behavior, trusted supply chain.                 |
| Sensitive Information Disclosure | LLMs revealing confidential data from training materials.               | Responses containing PII due to overfitting on the training data.  | Anonymize data, enforce access control.                                  |
| Insecure Plugin Design           | Vulnerabilities in plugins or extensions.                               | A third-party plugin causing SQL injections.                       | Security reviews, follow coding standards.                               |
| Excessive Agency                 | LLMs making uncontrolled decisions.                                     | An LLM customer service tool making unauthorized refunds.          | Limit LLM decisions, human oversight.                                    |
| Overreliance                     | Overreliance on LLMs for critical decisions without human oversight.    | An LLM making errors in customer service decisions without review. | Human review of LLM outputs, supplement with data inputs.                |
| Model Theft                      | Unauthorized access to proprietary LLM models.                          | A competitor downloading and using an LLM illicitly.               | Authentication, encrypt data, access control.                            |