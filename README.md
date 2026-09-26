# AI Colouring Book

The project aims to create a local system capable of creating a coloring book for the children aged around 10.

## About

The notebook draws wikipedia lead and potrait of famous people, creates a short biographie from the lead, compares the biographie against the lead, generates a coloable image and prints them on a page. The notebook uses Llama 3.1 8B to generate biographies, RoBERTa-Large MNLI as fact checker. Furthermore, it uses [Awacke1](https://huggingface.co/spaces/awacke1/Image-to-Line-Drawings) to generate line drawing, then redraws the drawing using Stable diffusion 1.5, ControlNet and IP-Adapter. 

## Technologies

Python 3.11

Jupyter Notebook

Ollama

Pytorch

Llama 3.1 8B

Roberta-Large MNLI

[Awacke1](https://huggingface.co/spaces/awacke1/Image-to-Line-Drawings)

Stable Diffusion 1.5

ControlnNet

IP-Adapter

## How it works

1. Accepts a name and crawls the wikipedia and extracts lead and potrait.
2. Generates atmost 6 sentences for biographie using Llam3.1 8B.
3. Checks the whether each sentence is supoorted by the lead.
4. Creates a Line drawing using [Awacke1,](https://huggingface.co/spaces/awacke1/Image-to-Line-Drawings) and Stable Diffusion 1.5 turns it into colorable drawing, guided by contolnet to follow the structure of the Line drawing, and IP-Adapter to keep the facial features.
5. Places the drawing and biographie on an A4 sheet.

The Image pipeline uses 512x640, UniPC, 40 steps, strength 0.57, guidance 9 and seed 42 plus the person's position in the list (43 in our notebook, since it is only tested on one person).

## Setup

To run the project on your own computer:

1. Clone the repository
  ```powershell
   git clone https://github.com/wilson257/AI_Colouring_Book_Main.git
   cd AI_Colouring_Book_Main/Local_Final_Run
  ```
2. Install the necessary libraries and [Ollama for Windows](https://ollama.com/download/windows)
  ```powershell
   py -3.11 -m venv .venv
   .\.venv\Scripts\python.exe -m pip install --upgrade pip
   .\.venv\Scripts\python.exe -m pip install torch==2.5.1 torchvision==0.20.1 --index-url https://download.pytorch.org/whl/cu121
   .\.venv\Scripts\python.exe -m pip install -r requirements.txt
   .\.venv\Scripts\python.exe -m ipykernel install --user --name coloring-book-local --display-name "Coloring Book Local"
  ```
3. Download Stable diffusion 1.5 into Local_Final_Run/stable-diffusion-v1-5-diffusers. 
  ```powershell
   .\.venv\Scripts\python.exe -c "from huggingface_hub import snapshot_download; snapshot_download('stable-diffusion-v1-5/stable-diffusion-v1-5', local_dir='stable-diffusion-v1-5-diffusers', allow_patterns=['*.json','tokenizer/*','feature_extractor/*','scheduler/*','unet/*fp16.safetensors','vae/*fp16.safetensors','text_encoder/*fp16.safetensors'])"
  ```
4. From Local_Final_Run folder, run  the following command
  ```powershell
   .\.venv\Scripts\python.exe -m jupyterlab
  ```
5. In `Local_Final_Run.ipynb`, select the Coloring Book Local kernel, and run all the cells. The first run needs internet, to download Llama 3.1 8B, the line drawing weight ([Awacke1),](https://huggingface.co/spaces/awacke1/Image-to-Line-Drawings) ControlNet, IP-Adapter, RoBERTa-large MNLI and for wikipedia.



## Output

The outputs are stored in `final_outputs/coloring_book.pdf` only if the biography passes the checker.

## Hardware

The target computer should have 6 GB graphics card and 16 GB RAM.

## Authors

Wilson Joel Aranha, Housam Mouloue, Melroy D'costa.
