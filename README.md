# EasyEspnet

Making Espnet easier to use.

## Requirements

We recommend using this Docker image which contains EVERYTHING you need to run EasyEspnet: `docker pull jindongwang/espnet:all11`


## Run

1. Prepare ESPnet data and add (train. val, test, token, prefix, bpemodel) information in data_load.data_config

2. Check or modify in train.py arg_list, config should be in ESPnet config style (remember to include decoding information if you want to compute cer/wer), run `python train.py`

3. Done. Results (log, model, snapshots) are saved in results_(dataset)/(config_name) by default.


## Distributed training
EasyEspnet supports multi-GPU training by default using Pytorch DataParallel, but it also supports PyTorch distributed parallel training which is much faster, for example, using 2 GPUs, 1 node: `CUDA_VISIBLE_DEVICES=0,1 python -m torch.distributed.launch --nproc_per_node=2 train.py --dist_train true`

## Decoding
set `--decoding_mode true` to perform decoding and CER/WER evaluation. For example: `python train.py --decoding_mode true`
