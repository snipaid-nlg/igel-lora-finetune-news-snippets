# Fine-Tune IGEL LoRA
This repository contains the sources for fine-tuning LoRA adapters for news snippet generation in german language with the IGEL model.

## How to use this code for continued instruction finetuning of IGEL

1. Get access to a GPU. E.g. rent 1 x RTX 4090 on [Vast.ai](https://vast.ai/).
2. Connect to the instance via ssh.

    ```ssh -i ~/.ssh/vastid_rsa -p <your_instance_port> root@<gpu_instance_ip>```
  
    > Note: At vast.ai connection setup is explained when connecting to a machine from the Instances section.

3. Clone this github repo.

    ```
    git clone https://github.com/snipaid-nlg/igel-lora-finetune-news-snippets.git
    cd igel-lora-finetune-news-snippets
    pip install -r requirements.txt
    ```
4. Start the continued fine-tuning.

    ```python finetune.py --base_model="malteos/bloom-6b4-clp-german" --data-path "./news-snippet-mlsum-instruct.csv"```
    
    > Note: The data-path supplies the path to the training data. In our case we train on an instruct dataset for news snippet generation. You can switch out this data by any other dataset with an instruction, input and output column.
5. Once Training finished, zip LoRA IGEL for download. In a terminal with connection to the GPU machine execute:

     ```
     apt-get install zip
     zip -r igel_finetuned.zip lora-igel/
     ```
    
 6. Download the zip file. In a second terminal with no remote connection execute:
 
    ```scp -i ~/.ssh/vastid_rsa -P <your_instance_port> root@<gpu_instance_ip>:igel-lora-finetune-news-snippets/igel_finetuned.zip ./Downloads/igel_finetuned.zip```
