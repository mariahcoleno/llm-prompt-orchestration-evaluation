## LLM Prompt Orchestration and Evaluation Framework

This project serves as a technical case study demonstrating LLM application design, prompt orchestration, multi-step generation workflows, and automated output validation.

As project lead, I designed the prompt workflow architecture, defined validation criteria, implemented fallback strategies, and evaluated model behavior across chained LLM interactions.

The framework demonstrates how structured prompting techniques can improve reliability, consistency, and quality control when building AI-powered applications.

### Features:
- **Prompt Chaining:** Implements multi-step LLM workflows where outputs from one stage become inputs for subsequent stages (question → answer → refined answer).
- **Few-Shot Prompt Design:** Uses examples within prompts to guide model behavior and improve output formatting.
- **Output Validation:** Applies automated checks to evaluate relevance, quality, and adherence to expected formats.
- **Fallback Logic:** Provides reliable responses when generated outputs fail validation criteria.
- **LLM Behavior Analysis:** Enables inspection of intermediate outputs to evaluate model performance and improve prompt strategies.
  
### Requirements
- Google Colab with GPU runtime (required for performance) 
- Python 3.x (pre-installed in Google Colab)
- `transformers` library (installed during setup)
- torch (required for GPU support in Colab)
- streamlit (only need for web demo)

### Files
- `requirements.txt`: Lists all Python dependencies required to run the techniques.
- `prompt_engineering.py`: The main script that uses the transformers library for prompt chaining and few-shot engineering with validation and fallback logic.

### Setup and Usage
1. Open the prompt_engineering.py script in Google Colab (https://colab.research.google.com/):
   - Go to Google Colab.
   - Since prompt_engineering.py is a Python script (.py) and not a notebook (.ipynb), you’ll need to create a new notebook to run the script:
     - Click File > New notebook in Drive to create a blank notebook.
   - Upload the file to the Colab file system: 
     - Click the Files tab on the left, then click the Upload button and upload prompt_engineering.py.
     - Alternatively, copy the contents of prompt_engineering.py (from your local machine or the GitHub repository) and paste them into a code cell in the notebook.
2. Set up GPU Runtime:
   - Go to Runtime > Change runtime type.
   - Select GPU as the hardware accelerator.
   - Click Save.
3. Install Dependencies: 
   - Add a new cell at the top of the notebook and run the following command to install dependencies from `requirements.txt`: `!pip install -r https://raw.githubusercontent.com/mariahcoleno/PromptEngineeringStage/main/requirements.txt`
   - If the above command fails (e.g., due to network issues or GitHub access), use this fallback:`!pip install transformers torch`
   - This ensures the required libraries are installed in the Colab environment.
4. Run the Script:
   - If the file is in the Colab environment (e.g., in the /content/ directory), you can execute it using a code cell with the command:`!python /content/prompt_engineering.py`
     - If you encounter a "file not found" error, double-check the file path and ensure the file is in the correct directory (e.g., /content/).
   - If you pasted the contents of prompt_engineering.py into a code cell, simply run that cell.
   - The script will use the GPU for faster inference.
 
### Note
- Running this project on a CPU (e.g., via terminal) is not recommended. Inference will be very slow or may fail for larger models like microsoft/phi-2.
- Google Colab provides free GPU access, but sessions may time out after inactivity. Save your work frequently.  

### Example Colab Output (phi-2 Model Repetition and Improved Answer, GPU)
- Below is a sample output from running the script in Google Colab with GPU enabled (`microsoft/phi-2` model).  
- This output demonstrates prompt chaining: the model first generates a question about "photosynthesis", then answers it, then refines the answer for clarity and simplicity.
- For the topic "photosynthesis":
  - The script prompts the model to generate a simple question for a 10-year old.
  - The model generates an answer, which is then refined to be even more accessible. 
  - Each step is validated; if the output fails validation, a fallback is used.  
  - In this example, the model's outputs passed validation, so the extracted and final outputs are the same.

Note: **Few-shot examples** are included in some prompts to help the model learn the desired format or reasoning style. This complements the prompt chaining approach by improving model reliability and output quality.

<details>
<summary>Click to expand Colab output</summary>

=== Prompt Sent to Model ===

Explain the following topic to a 10-year-old in 2 short sentences. Use simple words and include a real-world example.

Topic: Machine learning
A: It's when computers learn from examples to do tasks like guessing what's in a picture.

Topic: Photosynthesis
A: It's how plants make food from sunlight, like when a leaf turns sunshine into sugar.

Topic: Python
A: It's a programming language people use to tell computers what to do, like making games or apps.

Topic: Photosynthesis
A:

=== Full Model Output ===

Topic: Machine learning
A: It's when computers learn from examples to do tasks like guessing what's in a picture.

Topic: Photosynthesis
A: It's how plants make food from sunlight, like when a leaf turns sunshine into sugar. <-- (model repeats prompt answer)

Topic: Python
A: It's a programming language people use to tell computers what to do, like making games or apps.

Topic: Photosynthesis
A: Photosynthesis is when plants use sunlight to make food, like when plants use the sun's energy to make sugar from water and carbon dioxide. <-- (model generates improved answer)

=== Extracted Answer (improved model answer) ===
Photosynthesis is when plants use sunlight to make food, like when plants use the sun's energy to make sugar from water and carbon dioxide.

=== Validation Result ===
True

=== Final Output (Model Answer) ===
Photosynthesis is when plants use sunlight to make food, like when plants use the sun's energy to make sugar from water and carbon dioxide.

</details>

### To Modify the Example Colab Output:
- Change the `topic` variable in the script to test different queries.
- Edit the examples in the `build_prompt` function to tune the prompt for your use case.

### Project Structure
- prompt-engineering-techniques/
  - prompt_engineering_techniques/
    - README.md
    - app.py
    - prompt_engineering.py 
    - requirements.txt
  - .gitignore
  - requirements.txt (in repo root for Streamlit cloud, needed if add demo) 





