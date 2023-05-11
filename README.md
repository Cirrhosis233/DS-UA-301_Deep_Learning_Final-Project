# DS-UA-301_Final-Project

## Project Title: Music Classification and Generation

### Project Description

<img src="img\logic_path.jpg" style="zoom: 80%;" />

More Detailed explain in our presentation Slides: https://docs.google.com/presentation/d/1HeP6kb335AaxAfoemwWTdq9iRayCfWDOWrU6gUJZ7pA/edit?usp=sharing

**Goals**: Can there be some model structure that is performs well on:

- Multimodal Capability:
  - Audio - to - Text Classification
  - Text - to - Audio Generation
- Great generalization capability, once trained only some finetune needed
- No needs for expensive labeling

Our solution is to use **Joint embedding & Contrastive Learning**

And for Audio there is an open-source implementation called **CLAP**.

We have done some experiment to verify the generalization capability of CLAP, we choose **Harmonic CNN as our base Model**

And then finally we go back to Music Generation, using **Open-MusicLM** to generate some test music and see how it performs.

### Results

#### Compare Base Models to CLAP

<img src="img\acc.jpg" style="zoom: 80%;" />

#### Compare Music Generated

You can find music used to compare in `generation\compare` folder

#### Conclusion

<img src="img\conclusion1.jpg" style="zoom:80%;" />

<img src="img\conclusion2.jpg" style="zoom:80%;" />

### How to Run our Code

#### Base Model: HarmonicCNN

Just run the Jupyter Notebook located in `./classfication/BaseModel`, install the packages if needed

You should get an Accuracy for zero-shot classification of our Base Model

#### CLAP:

1. First install all dependencies required in `./classification/CLAP/CLAP-main/README.md`.
2. Download [630k-audioset-best.pt](https://huggingface.co/lukewys/laion_clap/blob/main/630k-audioset-best.pt) and put it into `./classification/CLAP/Checkpoint` folder
3. Download [dataset](https://drive.google.com/file/d/1osr5rcBfyxbTCC6jutHDwlfdwfiQghLk/view?usp=share_link), and extract it under `./classification/CLAP` and you should now have `./classification/CLAP/dataset` folder.
4. Our script to finetune the model is under `\classification\CLAP\CLAP-main\src\laion_clap\finetune-esc50.bat`, you’ll need to provide Weight&Bias account to run this.
5. You may run now run `./classification/CLAP/test.ipynb` to get some accuracy result, be sure to delete the `finetune_ckpt` parameter if you are not using finetuned model. I also marked this inside the notebook
6. We have modified some code in CLAP in order to load the fine-tuned models, the modified version of `hook.py` is under `\classification\CLAP\modified-hook.py`, you do not need to do anything since we already provided the modified version of whole repo, this is just a reminder that you may not successfully run our code if using the official CLAP repo.

#### Open-MusicLM

1. First install all dependencies required in `.\generation\open-musiclm-main\README.md`
2. Download all the files in https://drive.google.com/drive/u/0/folders/1347glwEc-6XWulfU7NGrFrYTvTnjeVJE and put them into `.\generation\open-musiclm-main\scripts\models` folder
3. Run `infer_top_match.bat` under `.\generation\open-musiclm-main\scripts\` folder to generate audios.

