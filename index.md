# DSC 180A Methodology Assignment 4

**Name:** Dylan Craver
**Email:** dcraver@ucsd.edu
**Section:** D26
**Mentor:** Lily Weng

---

**What is the most interesting topic covered in your domain this quarter?**
<br>
The most interesting topic was failure diagnosis in retrieval-augmented generation (RAG). A wrong final answer does not say which component failed: chunking, retrieval, reranking, or generation. RAGEC classifies errors by pipeline stage, and D2R-RAG separates "the retrieved evidence was insufficient" from "the model misused good evidence." I found it interesting that the right fix depends on the diagnosis, so detecting an error is only half the problem. This is also where cost matters, because rerunning the whole pipeline for every query is expensive.

**Describe a potential investigation you would like to pursue for your Quarter 2 Project.**
<br>
I would build and evaluate TrustRAG, a RAG framework that pairs evidence-based error detection with targeted, adaptive correction. The investigation would test it under three controlled evidence conditions: low distraction, missing support, and high distraction. It would also report an overcorrection rate, meaning how often a correct answer is wrongly "repaired." D2R-RAG does not control for evidence state or measure this harm, so its conclusions about when repair helps are limited. The main question is which repair strategies help in which evidence condition, and at what cost in latency and compute.

**What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**
<br>
Our reproduction of D2R-RAG's HotpotQA experiment scored 35.4% before repair and 39.8% after, using the authors' answer scorer. That scorer uses normalized answer containment rather than strict exact match, so a response can get credit while abstaining if it mentions the gold answer. I would add a stricter scorer and report both, plus the overcorrection rate. I would also run more than one seed, since a repeat run gave a slightly different gain (4.6 vs. 4.4 points), and extend beyond one dataset and one configuration. Our reproduction covers only the HotpotQA/LinUCB configuration, not every experiment in the paper.

**What other techniques would you be interested in using in your project?**
<br>
I would like to try evidence-quoting verification in the style of RLSeek, where the verifier must quote the supporting span at each step, as a detector inside TrustRAG. I would also like to try Doctor-RAG's prefix reuse and a distilled small diagnosis model to cut repair cost. Beyond those, I would compare the LinUCB bandit with other budget-aware strategies for choosing among repair actions, and add RAGEC-style stage classification so the repair is chosen from a specific error type.
