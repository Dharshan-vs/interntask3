# interntask3
# Python Screening Task 3 – Research Plan

## Research Plan

I'll start by looking at what's already out there for analyzing student code. After spending some time on Hugging Face and GitHub, I've found a few promising models like CodeBERT, PyCodeGPT, and GraphCodeBERT that seem like they could work for educational purposes. The tricky part is finding models that can actually understand student code - not just professional code - since students make different types of mistakes and think about problems differently.

My main criteria will be: can the model handle Python code well, does it understand natural language (for generating feedback), and can it be adapted for educational use? I'm particularly interested in models that can catch common student mistakes like off-by-one errors, infinite loops, and variable scoping issues. From what I've seen in the literature, most models are trained on professional codebases, so I'll need to be careful about how well they'll transfer to student-written code.

For testing, I'm planning to collect student code from a few different sources - GitHub Classroom submissions, some LeetCode student solutions, and hopefully some university programming courses if I can get access. I'm aiming for around 50,000 code samples, though honestly that might be optimistic depending on what I can actually get my hands on. I'll need to manually annotate these with competence levels (beginner/intermediate/advanced) and categorize the types of mistakes students make.

The real challenge will be evaluating whether these models can actually help students learn. Traditional metrics like accuracy and precision are important, but they don't tell me if the feedback is actually useful for learning. I'm thinking of trying an ensemble approach - combining different models since each one seems to have different strengths. I'll also need to get some actual teachers to test the system and see if the feedback makes sense to them and their students.

## Reasoning

**What makes a model suitable for high-level competence analysis?**

For competence analysis, I think the model needs to understand both what the code is doing (syntax) and what the student was trying to achieve (semantics). This is harder than it sounds because students often write code that works but isn't optimal, or they solve problems in creative ways that might not follow "best practices." 

The model should be able to handle different coding styles - some students are very verbose while others write extremely compact code. It also needs to distinguish between different types of mistakes: syntax errors vs. logic errors vs. just not knowing the "Pythonic" way to do something. Most importantly, it should give feedback that helps students think through problems themselves rather than just telling them the answer.

**How would you test whether a model generates meaningful prompts?**

This is where I think the real challenge lies. I can measure technical things like whether the model correctly identifies errors, but that doesn't tell me if the feedback is actually helpful for learning. I'm planning to test this by having teachers review the prompts and see if they think they'd be useful in their classrooms. 

I'll also try to measure things like: does the prompt help the student understand why their approach might not work? Does it encourage them to think about alternative solutions? Most importantly, does it avoid giving away the answer? I've seen some systems that are basically just error checkers - they tell you what's wrong but don't help you figure out how to fix it. That's not what I want to build.

**What trade-offs might exist between accuracy, interpretability, and cost?**

This is a big practical concern. The most accurate models are often "black boxes" - you can't really understand why they made a particular decision. But in education, teachers need to be able to trust and understand the system's reasoning, especially if they're going to use it to help students.

On the flip side, simpler, more interpretable models might not be as accurate, but at least you can see what they're thinking. There's also the cost issue - running these models isn't free, especially if you want real-time feedback. A student shouldn't have to wait 30 seconds to get feedback on their code. I'm probably going to have to make some compromises here, maybe using a simpler model for quick feedback and a more complex one for detailed analysis.

**Why did you choose the model you evaluated, and what are its strengths or limitations?**

I'm planning to test three different models: CodeBERT, GraphCodeBERT, and PyCodeGPT. Each one seems to have different strengths that could be useful for education. CodeBERT is good at understanding both code and natural language, which is important for generating feedback that students can actually understand. GraphCodeBERT looks at the structure of code (like how data flows through it), which could be really helpful for catching logic errors that students make. PyCodeGPT is specifically trained on Python code, so it might be better at catching Python-specific mistakes.

The problem is that each model has limitations too. CodeBERT doesn't really understand code structure, GraphCodeBERT is computationally expensive and might be overkill for simple errors, and PyCodeGPT might struggle with code that has comments or explanations. I'm thinking about trying to combine them somehow - maybe use different models for different types of analysis. But that adds complexity, and I'm not sure if the improvement would be worth the extra computational cost.

I'm also planning to try curriculum learning - starting with simple errors and gradually training on more complex problems. This might help the models learn student error patterns better than training on everything at once.

## Timeline (Realistically Speaking)

**Weeks 1-2: Getting Started**
- Try to collect student code samples - this is harder than I thought it would be. Most GitHub Classroom repos are private, and I'll need to figure out how to get access to university data ethically.
- Set up my development environment. I'll probably start with Google Colab since I don't have access to expensive GPU clusters.
- Learn how to properly parse Python code - the AST stuff is more complex than I initially realized.

**Weeks 3-4: First Model Tests**
- Try to fine-tune the models on whatever data I can get. I'm expecting this to be messy and probably won't work perfectly the first time.
- Run some basic evaluations to see if the models can even distinguish between beginner and advanced code.
- Start thinking about how to measure "pedagogical effectiveness" - this is going to be subjective.

**Weeks 5-6: Trying to Make It Better**
- Experiment with combining models, though I'm not sure if this will actually help or just make things more complicated.
- Try to get some teachers to test the system - this might be the hardest part since teachers are busy and skeptical of new tech.
- Hopefully fix some of the major bugs I'll inevitably introduce.

**Weeks 7-8: Polish and Hope**
- Try to make the system fast enough for real-time use, though I'm not sure if 2 seconds is realistic.
- Add some way for teachers to understand what the system is thinking.
- Test with actual students if I can find some willing participants.

## What I'm Actually Hoping For

**Data:**
- I'm aiming for around 50,000 code samples, but honestly, I'll take whatever I can get. Getting clean, annotated student code is surprisingly difficult.
- I'll try to get a mix of beginner, intermediate, and advanced code, though the exact numbers will depend on what's available.
- For errors, I'm expecting to see a lot of syntax mistakes and logic errors, with fewer style issues and algorithmic problems.

**Performance Goals:**
- I'd love to get 85% accuracy for competence classification, but I'd be happy with 70% for a first attempt.
- For misconception detection, anything above 60% precision would be great.
- I want the system to respond quickly, but I'm not sure if 2 seconds is realistic. Maybe 5-10 seconds would be more achievable.
- If teachers rate the feedback above 3/5, I'll consider that a success.

## References

**Models I'm planning to test:**
- CodeBERT: [https://huggingface.co/microsoft/codebert-base](https://huggingface.co/microsoft/codebert-base)
- GraphCodeBERT: [https://huggingface.co/microsoft/graphcodebert-base](https://huggingface.co/microsoft/graphcodebert-base)  
- PyCodeGPT: [https://huggingface.co/madlag/pycodegpt](https://huggingface.co/madlag/pycodegpt)

**Datasets I'm hoping to use:**
- CodeNet (IBM's code dataset): [https://github.com/IBM/Project_CodeNet](https://github.com/IBM/Project_CodeNet)
- EdNet (educational data): [https://github.com/riiid/ednet](https://github.com/riiid/ednet)

**Papers that inspired this approach:**
- Feng, Z., et al. (2020). CodeBERT: A Pre-Trained Model for Programming and Natural Languages. EMNLP 2020.
- Guo, D., et al. (2021). GraphCodeBERT: Pre-training Code Representations with Data Flow. ICLR 2021.

**Tools I'll probably use:**
- Hugging Face Transformers library
- Google Colab for initial experiments
- Python's AST module for code parsing
