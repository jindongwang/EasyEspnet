# EasyEspnet

Making Espnet easier to use.

## Requirements

We recommend using this Docker image which contains EVERYTHING you need to run EasyEspnet: `docker pull jindongwang/espnet:all11`


## Run

1. Prepare ESPnet data and add (train. val, test, token, prefix, bpemodel) information in data_load.data_config

2. Check or modify in train.py arg_list, config should be in ESPnet config style (remember to include decoding information if you want to compute cer/wer), run `train.py`. for example, `python train.py --root_path an4/asr1 --dataset an4`

3. Done. Results (log, model, snapshots) are saved in results_(dataset)/(config_name) by default.


## Distributed training
EasyEspnet supports multi-GPU training by default using Pytorch DataParallel, but it also supports PyTorch distributed parallel training which is much faster, for example, using 2 GPUs, 1 node: `CUDA_VISIBLE_DEVICES=0,1 python -m torch.distributed.launch --nproc_per_node=2 train.py --root_path an4/asr1 --dataset an4 --dist_train true`

## Decoding
set `--decoding_mode true` to perform decoding and CER/WER evaluation. For example: `python train.py --root_path an4/asr1 --dataset an4 --decoding_mode true`


## Demo
We provide the processed features using an4 as demo.

To run this demo, please execute:
1. Download and unzip the features `mkdir data; cd data; wget https://transferlearningdrive.blob.core.windows.net/teamdrive/dataset/speech/an4_features.tar.gz; tar -zxvf an4_features.tar.gz; rm an4_features.tar.gz; cd ..`
2. Start training with EasyEspnet: `python train.py --root_path data/an4/asr1/ --dataset an4`