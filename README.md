# CHAN-DST

Code for our ACL 2020 paper: **A Contextual Hierarchical Attention Network with Adaptive Objective for Dialogue State Tracking. Yong Shan, Zekang Li, Jinchao Zhang, Fandong Meng, Yang Feng, Cheng Niu, Jie Zhou. ACL 2020 *(Long)***. [[arxiv](https://arxiv.org/abs/2006.01554)]

## Abstract
Recent studies in dialogue state tracking (DST) leverage historical information to determine states which are generally represented as slot-value pairs. However, most of them have limitations to efficiently exploit relevant context due to the lack of a powerful mechanism for modeling interactions between the slot and the dialogue history. Besides, existing methods usually ignore the slot imbalance problem and treat all slots indiscriminately, which limits the learning of hard slots and eventually hurts overall performance. In this paper, we propose to enhance the DST through employing a contextual hierarchical attention network to not only discern relevant information at both word level and turn level but also learn contextual representations. We further propose an adaptive objective to alleviate the slot imbalance problem by dynamically adjust weights of different slots during training. Experimental results show that our approach reaches 52.68% and 58.55% joint accuracy on MultiWOZ 2.0 and MultiWOZ 2.1 datasets respectively and achieves new state-of-the-art performance with considerable improvements (+1.24% and +5.98%).

<p align="center"><img src="https://i.loli.net/2020/06/05/rsEHlLake37SdoY.jpg" width="80%" class="center"/></p>

## Requirements
* python 3.6
* pytorch >= 1.0
* Install python packages:
  - ``pip install -r requirements.txt``

## Usages
### Data Preprocessing
We conduct experiments on the following datasets:
* MultiWOZ 2.0 [Download](https://www.repository.cam.ac.uk/bitstream/handle/1810/280608/MULTIWOZ2.zip?sequence=3&isAllowed=y)
* MultiWOZ 2.1 [Download](https://www.repository.cam.ac.uk/bitstream/handle/1810/294507/MULTIWOZ2.1.zip?sequence=1&isAllowed=y)

We use the same preprocessing steps for both datasets. For example, preprocessing Multiwoz 2.0:
```bash
$ pwd
/home/user/chan-dst
# download multiwoz 2.0 dataset
$ wget https://www.repository.cam.ac.uk/bitstream/handle/1810/280608/MULTIWOZ2.zip?sequence=3&isAllowed=y -O multiwoz2.0.zip
# preprocess datasets for training DST and STP jointly
$ unzip -j multiwoz2.0.zip -d data/multiwoz-update/original
$ cd data/multiwoz-update/original
$ mv ontology.json ..
$ python convert_to_glue_format.py
# preprocessing datasets for fine-tuning DST with adaptive objective
$ unzip -j multiwoz2.0.zip -d data/multiwoz/original
$ cd data/multiwoz/original
$ mv ontology.json ..
$ python convert_to_glue_format.py
```

For Multiwoz 2.1, replace the corresponding directories with `multiwoz2.1-update` and `multiwoz2.1`, respectively.

### Train
Take MultiWOZ 2.0 as an example.

1. Pre-training

    ```bash
    bash run_multiwoz2.0.sh
    ```

2. Fine-tuning

    ```bash
    bash run_multiwoz2.0_finetune.sh
    ```

## Citation
If you find this code useful, please cite as:

```
@inproceedings{shan2020contextual,
  title={A Contextual Hierarchical Attention Network with Adaptive Objective for Dialogue State Tracking},
  author={Shan Yong, Li Zekang, Zhang Jinchao, Meng Fandong, Feng Yang, Niu Cheng, Zhou Jie},
  booktitle={Proceedings of the 58th Conference of the Association for Computational Linguistics},
  year={2020}
}
```
