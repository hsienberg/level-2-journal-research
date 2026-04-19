# Disease Detectives

## 1. What I Built

This project is a Hugging Face Space designed to help identify diseases from symptoms and images using an AI model. A user types in a description of their symptoms — including how long they have had them, how severe they feel, and any relevant background — and optionally uploads a photo of a visible condition like a rash or swelling. The Space then returns a ranked list of possible conditions, an explanation of which symptoms match each condition, and a recommendation for what to do next.

The design choice that matters most is the use of a large, general-purpose language model (Claude via the Anthropic API) rather than a small, task-specific model trained on a narrow medical dataset. This was a deliberate response to a problem discovered earlier in the project: smaller, specialized models on Hugging Face produced inaccurate and inconsistent results when tested with real symptom combinations. The current version is functional and running, though it is still early-stage and the accuracy has not been formally evaluated yet.

---

## 2. My Research Question

**How can AI-assisted tools be made more accurate for medical symptom diagnosis, particularly for diseases that are commonly identified too late?**

This question grew out of two experiences that happened close together. The first was a comparative analysis of two existing medical diagnosis models on Hugging Face — `segadeds/Medical_Diagnosis` and `khalednabawi11/Medical-Scan-Gemma` — which both failed to correctly identify hypothyroidism from its classic symptoms. The second was participation in Science Olympiad's Disease Detectives event, where the cases studied were often ones that had been identified too late to prevent serious harm. These two experiences together pointed toward the same gap: current AI diagnostic tools are not reliable enough, especially for conditions that are not the most obvious or common.

---

## 3. Why This Matters to Me

Medicine is a field I am actively pursuing. I compete in Science Olympiad's biology events, including Disease Detectives and Anatomy and Physiology, and those events have introduced me to diseases I had never heard of before — and to the real consequences of late diagnosis. Hypothyroidism is a good example of something personal here: it is a condition where the thyroid does not produce enough T4, it affects millions of people, and yet the models I tested could not identify it from its most well-known symptoms. That bothered me.

I am also a self-described paranoid person when it comes to health, which means I actually use tools like this. I am not building it as an abstract exercise — I want it to work. That personal investment shapes how I think about accuracy: it is not just a metric, it is the difference between a tool that is actually useful and one that gives someone the wrong answer when they are worried about their health.

---

## 4. What I Tried

**Testing Existing Models (Week 2)**

Before building anything, I tested two existing medical diagnosis models on Hugging Face to understand the baseline.

| Input | Model | Output | Accurate? |
|---|---|---|---|
| "cold, weight gain" | khalednabawi11/Medical-Scan-Gemma | Anemia | No |
| "weight gain, cold" (order switched) | khalednabawi11/Medical-Scan-Gemma | Malaria | No |
| Image of a goiter | segadeds/Medical_Diagnosis | "Everything healthy" | No |

I expected both models to identify hypothyroidism, since cold intolerance and unexplained weight gain are two of its most documented symptoms. Neither model did. What made it worse was that switching the order of the same two symptoms produced a completely different wrong answer — which suggests the model is pattern-matching on word order rather than reasoning about symptom combinations.

**Building My Own Space (Weeks 3–5)**

After seeing those failures, I started building a Space of my own using Claude to generate the Python code. This involved multiple rounds of debugging — runtime errors, build conflicts with Gradio and Python 3.13 compatibility, and authentication issues with the Anthropic API. The final version uses a system prompt that instructs the model to organize its response into clear sections: possible conditions, symptom analysis, and recommended actions.

I also built several supporting tools during this period, including a Medical Entity Extractor and a Medical Text Generator, to explore what kinds of outputs were useful and which ones were too noisy or unfocused.

---

## 5. What I Learned

The most important thing I learned is that model size and training specificity are in tension with each other in a way that is not obvious at first. I assumed that a model trained specifically on medical data would outperform a general model on medical questions. The opposite turned out to be true — at least for the models I tested. The specialized models had been trained on too narrow a slice of diseases and symptoms, which made them brittle. They worked for the most basic cases and failed on anything slightly less common.

The general-purpose model, given a well-written system prompt, handled nuance much better. This shifted how I think about building AI tools: the prompt and the framing matter as much as the underlying model, sometimes more.

---

## 6. What Still Needs Work / Who It Might Fail For

**Unfinished parts:**
- The Space has not been tested with a systematic set of diseases to measure real accuracy. Right now, I know it works better than the models I compared it against, but I do not have numbers to back that up.
- There is no feedback mechanism — users cannot flag a wrong answer, which means there is no way to improve the tool over time based on real use.

**Where it might fail:**
- Rare diseases are still a problem. A general language model is trained on the internet, which over-represents common conditions. Someone presenting with a rare disease may still get a wrong or vague answer.
- The tool relies entirely on what the user describes. If someone does not know the right words for their symptoms, or leaves out something important, the output will be less accurate.
- There is no access to lab values, medical history, or physical exam findings — all of which real doctors use. Symptom-only diagnosis has a hard ceiling on accuracy regardless of how good the model is.
- The tool could be more dangerous for people who take its output as a final answer rather than a starting point. The disclaimers help, but they do not solve the problem.

---

## 7. Sources to Add or Cite

1. **Model cards for the two tested models** — `segadeds/Medical_Diagnosis` and `khalednabawi11/Medical-Scan-Gemma` on Hugging Face. These should be cited directly since they were tested as part of this project.

2. **Research on symptom-based diagnostic AI accuracy** — There is published work comparing AI diagnostic tools to physician diagnosis (search: "large language models clinical diagnosis accuracy" in Google Scholar or PubMed). A 2023 or 2024 paper would be most relevant.

3. **Anthropic's Claude model documentation** — The system prompt design used in this project is based on Claude's capabilities. The Anthropic model card or usage documentation is worth citing.

4. **CDC or NIH resources on hypothyroidism** — Since hypothyroidism is the specific test case used in Week 2, a clinical source on its symptoms would strengthen the argument that the models should have caught it.

5. **Work on training data bias in medical AI** — Search: "medical AI training data bias underrepresented diseases." There is a growing body of research on how rare and underrepresented conditions are systematically missed by models trained on imbalanced datasets. This connects directly to the limitation you identified.

---

## Revision Notes

**Strongest parts of this draft:**
- Section 4 (What I Tried) is the most grounded because you gave specific, testable evidence: real model names, real symptom inputs, and real wrong outputs. The table format makes the failure clear.
- Section 3 (Why This Matters) is strong because the Science Olympiad connection and the personal motivation are specific to you — that is the kind of detail that makes a student paper feel real instead of generic.

**Parts that still need more evidence from you:**
- Section 5 (What I Learned) is currently a logical conclusion drawn from your notes, but it would be stronger if you added one sentence in your own words about the moment your thinking actually shifted.
- Section 6 is honest but thin — if you have tested any edge cases or gotten any outputs that surprised you (good or bad), add them here.

**Parts that sound too generic and should be rewritten in your own words:**
- The last paragraph of Section 1 uses phrases like "functional and running" and "formally evaluated" that sound like a report. Replace with how you would actually describe the Space to a classmate.
- The opening of Section 2 is clean but a little stiff. Try reading it out loud — if it sounds like you wrote it, keep it; if it sounds like an AI wrote it, rewrite it in your voice.
