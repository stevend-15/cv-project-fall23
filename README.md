# cv-project-fall23
Computer Vision project repo

## test GAN with MINST
```
test.sh
```
## Train on MOT20
Below are steps to train FairMOT on the MOT20 dataset using the pre-trained model. 

1. Open the FairMOT [README](https://github.com/ifzhang/FairMOT#readme)
2. Copy the steps within the README to [set up the Conda environment and DCNv2 backbone](https://github.com/ifzhang/FairMOT#installation)
3. Download the MOT20 dataset using [this link](https://motchallenge.net/data/MOT20.zip) into `FairMOT-master/FairMOT-master/src/lib/datasets`. 

```
wget https://motchallenge.net/data/MOT20.zip
```


4. Unzip that MOT20 file
5. Restructure the data according to the instructions [here](https://github.com/ifzhang/FairMOT#data-preparation)
6. Navigate to `src/gen_labels_20.py` and open it
7. Using your file explorer, copy the path to the `MOT20` folder to your clipboard. Ex: `/home/grads/stedevert33/cv/project/cv-project-fall23/FairMOT-master/FairMOT-master/src/lib/datasets/MOT20`
8. Find the lines of `gen_labels20.py` where the `seq_root` and `label_root` are being set. Changed those lines to use the copied path. Ex: 
```
seq_root = '/home/grads/stedevert33/cv/project/cv-project-fall23/FairMOT-master/FairMOT-master/src/lib/datasets/MOT20/images/train'
label_root = '/home/grads/stedevert33/cv/project/cv-project-fall23/FairMOT-master/FairMOT-master/src/lib/datasets/MOT20/labels_with_ids/train'
```
9. `cd` to the `src` directory if you weren't already there
10. Run `python gen_labels20.py`. Execution may take a few seconds. 
11. Now it is time to make room for the pre-trained model. Navigate back to `FairMOT-master/FairMOT-master`
12. `mkdir models`
13. Download the `fairmot_dla34.pth` model from [this google drive](https://drive.google.com/file/d/1SFOhg_vos_xSYHLMTDGFVZBYjo8cr2fG/view) to your local computer. 
14. `scp` that file to your Glogin. Ex: `scp fairmot_dla34.pth stedevert33@glogin.cs.vt.edu:~`
15. Move that file to the newly created `models` directory. 
16. Modify `src/cfg/mot20.json` to reflect your path to the `datasets` folder where `MOT20` resides. Ex: 

```
"root":"/home/grads/stedevert33/cv/project/cv-project-fall23/FairMOT-master/FairMOT-master/src/lib/datasets/",
```
17. `chmod +x experiments/mot20_ft_mix_dla34.sh`
18. Run `experiments/mot20_ft_mix_dla34.sh`