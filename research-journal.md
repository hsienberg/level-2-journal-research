## Week [2] — [Training Data and Representation]

### This Week's Method
In class we learned about comparative analysis. We used the same question with different tools and observe where they agreed or disagreed. This method is used to further understand what the AI tool can and cannot see. We used feelings from Eckman's six feelings that everyone "apparently" feels and inserted them into a tool. We kept trying with different prompts and further analyzed the answers that it produced. 

### How I Applied It
I am interested in the medical field currently and I found out that if I go to hugging face, I can interact with different models there. The two models that I found were segadeds/Medical_Diagnosis and khalednabawi11/Medical-Scan-Gemma. I tested both with symptoms regarding hypothyroidism, which is a severe thryoid disease in which you do not produce enough T4 for the body. 

### What I Expected
I expected both models to predict the disease of hypothyoridism accurately. It is a very common disease in the United States, so I assumed that this chatbot would definitely give me a correct diagnosis. 

### What I Found
The second model listed above gave me anemia when I put the following cold, weight gain. If I switched cold and weight gain it becomes malaria. The problem is that if you put anemia, you actually do not get weight gain at all. This model is inaccurate while the other one I inputted a picture of a goiter and it said that everything was healthy. 

### Why I Think This Happened
I think that the training data is completely too specific for the model. It was trained to the most BASIC symptoms and needs. It did not show any accuracy due to the fact that it had the broadest diseases and none of the more niche or specific life-threatening diseases. 


## Week [3] — [Space Exploring]

### This Week's Method
In class we learned how to make a space. We can use the API with AI to help us create some code in the spaces. We can create a whole new model just for our personal needs with AI. AI can help us create the model. 

### How I Applied It
I am interested in the medical field currently and I found out that if I go to hugging face, I can create my own space. I actually downloaded Claude because to me it was more reliable than ChatGPT or Gemini and I began coding with AI with API formatting. It was pretty cool but I still need to get used to it. 

### What I Expected
I expected both models to show the results immediately but none of that happened. I had to run multiple trial-and-error runs to ultimately achieve what I wanted out of the code, because AI makes a lot of mistakes. 

### What I Found
I found out that AI can code for many things simply with Hugging Face, and this inspired me to make more. I also found that these are what people at Hugging Face do, using AI or manually coding for the spaces that we see today. 

### Why I Think This Happened
I think this happened due to the code. The code causes everything and produces the spaces that are present in Hugging Face. The errors happened because AI can be faulty sometimes and just needs some more nudging in the right direction. 


### Limitations
It only has the most common or easy to treat diseases and none of the life-threatening diseases that most people tend to worry about. 

### What I Want to Try Next
I want to learn and create a model that can accurately identify medical issues accurately and in depth. 


## Week [4] — [Space Creation]

### This Week's Method
We tried to code for a space using Claude or any AI model that will put our thoughts into a Hugging Face Space. You can talk to Claude, for example, and it will generate some Python code that you can insert into the HuggingFace spaces.  We had to input this code into the files which were app.py and some of the other files that were present. Mr. Plate also explained what each file was and how to use them. 

### How I Applied It
I am interested in the medical field currently and I am an active participant in Science Olympiad. I actually specialize in all of the biology events such as Disease Detectives and Anatomy and Physiology. Disease Detectives had a significant impact on me because I learned some diseases that I have never before and all of the cases that were presented were identified too late. I thought about a new idea which uses an AI model that can detect early which can help prevent fatal symptoms. 

### What I Expected
I expected the model or the code to run properly but it encountered a runtime error because the hugging space library is too small and can not hold the code that I inputted via Claude. 

### What I Found
I found out that I need to reduce some memory limits and some authentication that needs to be fixed before the idea of Disease Detectives come to life. 



## Week [5] — [Developing Side Spaces]

### This Week's Method
We tried to code for a space using Claude or any AI model that will put our thoughts into a Hugging Face Space. You can talk to Claude, for example, and it will generate some Python code that you can insert into the HuggingFace spaces.  I created numerous programs  such as medical Entity Extractor, Medical Text Generator, and a Dictonary. I used Claude and inputted my thinking into the generative AI textbox. It then sputed out a code which I had to debug before inputting it inside my Space.

### How I Applied It
I am interested in the medical field currently and I personally created all of these generators/extractors to help me diagnose some diseases. I am a very paranoid person so I plug into diseases all the time in this. I can improve this further to be more specific later on. 

### What I Expected
I expected the model or the code to run properly to be a little more not that vivid because the Medical Text Generator gave me a very vivid color and highlighted any word that "stood out". It did not really meet what I really wanted since I wanted something that can detect words that are actually helpful and not also detect trash words. 

### What I Found
I found out that AI is very faulty and we need to keep improving if we want it to be the best specific thing. 

### Why I Think This Happened
I think that I did not really specify enough to make the AI meet my needs and it was just a baseline that I created. I feel like next time I should give it a deeper analysis and what I want so it can spit what I am expecting.




## Week [6] — [Debugging Errors]
 
### This Week's Method
This week we focused on debugging errors that appear when deploying code to Hugging Face Spaces. The method involved reading runtime and build error logs carefully, identifying the root cause of each failure, and making targeted fixes to the code or configuration files. Rather than rewriting everything from scratch, we learned to isolate the specific line or dependency causing the problem and adjust only what was necessary.
 
### How I Applied It
I was actively trying to get my disease identification Space to go live. After uploading my `app.py` and `requirements.txt`, the Space kept failing at either the build stage or the runtime stage. I used Claude to help me read the error logs and figure out what each one meant, then applied fixes one at a time. Each fix either solved the problem or revealed the next one underneath it.
 
The three errors I ran into were:
 
**Error 1 — Runtime crash: `ModuleNotFoundError: No module named 'audioop'`**
Gradio depends on a library called `pydub`, which in older Python versions used a built-in module called `audioop`. Python 3.13 removed that module entirely, so when Hugging Face tried to start the app, it crashed immediately before anything even loaded.
 
**Error 2 — Build conflict: `Cannot install gradio==4.42.0 and gradio==4.44.0`**
My first fix was to pin Gradio to an older version (`4.42.0`) in `requirements.txt` to avoid the `audioop` issue. This caused a new problem: Hugging Face forces its own version of Gradio (`4.44.0`) during the build, so having two conflicting version requirements made the build fail entirely.
 
**Error 3 — Missing package: `No matching distribution found for pyaudioop`**
My second fix was to add `pyaudioop` as a dependency, since it is a backport of the missing module. This also failed — `pyaudioop` does not exist as an installable pip package at all, so the build crashed again trying to find it.
 
### What I Expected
I expected that once the code was written and uploaded, the Space would build and run cleanly. I also expected that each fix I applied would solve the problem for good. Instead, every fix uncovered a new error underneath it, which was frustrating but also ended up being a real lesson in how layered software dependencies actually work.
 
### What I Found
The actual solution was not to install anything new or pin any version — it was to patch the missing module directly inside `app.py` before Gradio ever tried to load. By adding these lines at the very top of the file:
 
```python
import sys
import types
if 'audioop' not in sys.modules:
    sys.modules['audioop'] = types.ModuleType('audioop')
if 'pyaudioop' not in sys.modules:
    sys.modules['pyaudioop'] = types.ModuleType('pyaudioop')
```
 
Python is tricked into thinking the module already exists, so Gradio never crashes looking for it. The `requirements.txt` was simplified back to just `anthropic` and `Pillow`, letting Hugging Face handle Gradio on its own.
 
### Why I Think This Happened
The root cause was a version mismatch between the Python environment Hugging Face uses (Python 3.13) and the dependencies that Gradio was built for. Hugging Face updated to Python 3.13, but Gradio's audio dependency (`pydub`) had not caught up yet. This is a common problem in software development — when one part of the stack updates, something else breaks. My fixes kept trying to solve the symptom (the missing module) by installing things, when the real fix was to intercept the problem before it happened. It took three rounds of trial and error to get there, but understanding *why* each fix failed made the final solution make sense.
