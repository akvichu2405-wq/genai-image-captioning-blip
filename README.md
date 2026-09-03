## Prototype Development for Image Captioning Using the BLIP Model and Gradio Framework
### DATE: 03/09/2026
### AIM:
To design and deploy a prototype application for image captioning by utilizing the BLIP image-captioning model and integrating it with the Gradio UI framework for user interaction and evaluation.

### PROBLEM STATEMENT:

### DESIGN STEPS:

### STEP 1:
Install libraries; secure API key for model access.
### STEP 2: 
Define function to send image to API, get caption.
### STEP 3: 
Create utility to convert PIL image to base64 string.
### STEP 4:  
Write captioner function to process image and call API.
### STEP 5: 
Build Gradio interface with Image Input, Text Output.
### STEP 6:
Launch the application and verify captioning functionality.
### PROGRAM:
```
# Install dependencies if required:
# pip install -U gradio google-genai pillow python-dotenv

import os
import gradio as gr
from google import genai
from dotenv import load_dotenv

# Load API key from .env file
load_dotenv()

api_key = os.getenv("GEMINI_API_KEY")

if not api_key:
    raise ValueError("GEMINI_API_KEY not found in .env file")

# Create Gemini client
client = genai.Client(api_key=api_key)


# Image Captioning Function
def captioner(image):

    if image is None:
        return "Please upload an image."

    try:
        prompt = "Write a short, descriptive caption for this image."

        response = client.models.generate_content(
            model="gemini-3.6-flash",
            contents=[image, prompt]
        )

        return response.text

    except Exception as e:
        return f"Error: {str(e)}"


# Create Gradio Interface
gr.close_all()

demo = gr.Interface(
    fn=captioner,
    inputs=[
        gr.Image(
            label="Upload image",
            type="pil"
        )
    ],
    outputs=[
        gr.Textbox(
            label="Caption",
            lines=3
        )
    ],
    title="Image Captioning with Gemini",
    description="Upload an image to generate a descriptive caption using Gemini."
)

# Launch application
demo.launch()
```

### OUTPUT:
<img width="917" height="437" alt="image" src="https://github.com/user-attachments/assets/914ea341-acaa-48d0-a1a2-653b986eb6e8" />

### RESULT:
The BLIP model was successfully integrated with the Gradio framework, resulting in the deployment of a functional web application for image captioning.
