# IRN

This is the original PyTorch implementation of the following work: **Irregularity Reflection Neural Network for Multivariate Time Series Forecasting**. 
## Content
 - Datasets
 - Requirements
 - Dataset preparation
 - Pretrain preparation
 - Run Train code
 - Run Pretrain testing code
## Features
- [x] Support **11** popular time-series forecasting datasets.  

![traffic](https://img.shields.io/badge/🚅-Traffic-yellow)
![electric](https://img.shields.io/badge/%F0%9F%92%A1-Electricity-yellow)
![Solar Energy](https://img.shields.io/badge/%F0%9F%94%86-Solar%20Energy-yellow)
![finance](https://img.shields.io/badge/💵-Finance-yellow)
- [x] Provide all training logs.
- [x] Support RevIN to handle datasets with a large train-test sample distribution gap. To activate, simply add ```--RIN True``` to the command line. [**Read more**](./docs/RevIN.md)


## Datasets

We conduct the experiments on **11** popular time-series datasets, namely **Electricity Transformer Temperature (ETTh1, ETTh2 and ETTm1) ,  PeMS (PEMS03, PEMS04, PEMS07 and PEMS08) and Traffic, Solar-Energy, Electricity and Exchange Rate**, ranging from **power, energy, finance and traffic domains**. 


### Overall information of the 11 datasets

| Datasets      | Variants | Timesteps | Granularity | Start time | Task Type   |
| ------------- | -------- | --------- | ----------- | ---------- | ----------- |
| ETTh1         | 7        | 17,420    | 1hour       | 7/1/2016   | Multi-step  |
| ETTh2         | 7        | 17,420    | 1hour       | 7/1/2016   | Multi-step  |
| ETTm1         | 7        | 69,680    | 15min       | 7/1/2016   | Multi-step  |
| PEMS03        | 358      | 26,209    | 5min        | 5/1/2012   | Multi-step  |
| PEMS04        | 307      | 16,992    | 5min        | 7/1/2017   | Multi-step  |
| PEMS07        | 883      | 28,224    | 5min        | 5/1/2017   | Multi-step  |
| PEMS08        | 170      | 17,856    | 5min        | 3/1/2012   | Multi-step  |
| Traffic       | 862      | 17,544    | 1hour       | 1/1/2015   | Single-step |
| Solar-Energy  | 137      | 52,560    | 1hour       | 1/1/2006   | Single-step |
| Electricity   | 321      | 26,304    | 1hour       | 1/1/2012   | Single-step |
| Exchange-Rate | 8        | 7,588     | 1hour       | 1/1/1990   | Single-step |


### Requirements

Install the required package first:

```
cd IRN
conda create -n irn python=3.8
conda activate irn
pip install -r requirements.txt
```
**caution**
Pytorch version is very sensitive, therefore you need to download pytorch 1.8.0 according to OS version, GPU series, and cuda version.


### Dataset preparation

<!-- All datasets can be downloaded [here](https://drive.google.com/drive/folders/1RIQ5V1yOojvkf2R4yh2MotFF_p5QmoTk?usp=sharing).  -->
To prepare the datasets, run shell script prepare_data.sh:
```
source prepare_data.sh
```
The data directory structure is shown as follows. 
```
datasets
 ┣ ETT-data
 ┃ ┣ ETTh1.csv
 ┃ ┣ ETTh2.csv
 ┃ ┗ ETTm1.csv
 ┣ PEMS
 ┃ ┣ PEMS03.npz
 ┃ ┣ PEMS04.npz
 ┃ ┣ PEMS07.npz
 ┃ ┗ PEMS08.npz
 ┗ financial
 ┃ ┣ electricity.txt
 ┃ ┣ exchange_rate.txt
 ┃ ┣ solar_AL.txt
 ┃ ┗ traffic.txt

```

### Pretrain preparation
<!-- All datasets can be downloaded [here](https://drive.google.com/drive/folders/1XmTj18Abjv2FUizPb2zqvImrDmScIYn6?usp=sharing).  -->
To prepare the pretrain models, run shell script prepare_data.sh:
```
source prepare_pretrainmodel.sh
```
The result of above shell script is as below.
```
checkpoints
 ┣ ETTh1
 ┃ ┣ multi
 ┃ ┃ ┣ seq168
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq336
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq720
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ single
 ┃ ┃ ┣ seq168
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq336
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq720
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┣ ETTh2
 ┃ ┣ multi
 ┃ ┃ ┣ seq168
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq336
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq720
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ single
 ┃ ┃ ┣ seq168
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq336
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq720
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┣ ETTm1
 ┃ ┣ multi
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq288
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq672
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq96
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ single
 ┃ ┃ ┣ seq24
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq288
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq48
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┣ seq672
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┃ ┃ ┗ seq96
 ┃ ┃ ┃ ┗ bestmodel.pth
 ┣ PEMS
 ┃ ┣ 03
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ 04
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ 07
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ 08
 ┃ ┃ ┗ bestmodel.pth
 ┣ electricity
 ┃ ┣ seq12
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq24
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq3
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ seq6
 ┃ ┃ ┗ bestmodel.pth
 ┣ exchange
 ┃ ┣ seq12
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq24
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq3
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ seq6
 ┃ ┃ ┗ bestmodel.pth
 ┣ solar
 ┃ ┣ seq12
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq24
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq3
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ seq6
 ┃ ┃ ┗ bestmodel.pth
 ┗ traffic
 ┃ ┣ seq12
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq24
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┣ seq3
 ┃ ┃ ┗ bestmodel.pth
 ┃ ┗ seq6
 ┃ ┃ ┗ bestmodel.pth

```

## Run Train code

We mainly refer to [SCINET](https://github.com/cure-lab/SCINet) which conducts all experiments. We follow the same settings of [StemGNN](https://github.com/microsoft/StemGNN) for PEMS 03, 04, 07, 08 datasets, [MTGNN](https://github.com/nnzhan/MTGNN) for Solar, electricity, traffic, financial datasets, [Informer](https://github.com/zhouhaoyi/Informer2020) for ETTH1, ETTH2, ETTM1 datasets. The detailed training commands are given as follows. 
#### For ETTH1 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 168 --label_len 24 --pred_len 24 --hidden-size 0.5 --stacks 1 --levels 3 --lr 1e-3 --batch_size 64 --dropout 0.5 --model_name etth1_M_I48_O24_lr3e-3_bs8_dp0.5_h4_s1l3 --train_model IRN_c_6_F_3  --evaluate False
```
multivariate, out 48
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 3 --lr 0.003 --batch_size 16 --dropout 0.25 --model_name etth1_M_I96_O48_lr0.009_bs16_dp0.25_h4_s1l --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 168
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 4 --stacks 1 --levels 3 --lr 5e-4 --batch_size 32 --dropout 0.5 --model_name etth1_M_I336_O168_lr5e-4_bs32_dp0.5_h4_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 336
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 6e-4 --batch_size 512 --dropout 0.5 --model_name etth1_M_I336_O336_lr1e-4_bs512_dp0.5_h1_s1l4 --train_model IRN_c_8_F_5 --evaluate False
```
multivariate, out 720
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 1 --stacks 1 --levels 5 --lr 5e-5 --batch_size 64 --dropout 0.5 --model_name etth1_M_I736_O720_lr5e-5_bs256_dp0.5_h1_s1l5 --train_model IRN_c_6_F_3 --evaluate False
```
Univariate, out 24
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 64 --label_len 24 --pred_len 24 --hidden-size 8 --stacks 1 --levels 3 --lr 0.007 --batch_size 64 --dropout 0.26 --model_name etth1_S_I64_O24_lr0.007_bs64_dp0.25_h8_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```
Univariate, out 48
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 4 --lr 0.0001 --batch_size 8 --dropout 0.5 --model_name etth1_S_I720_O48_lr0.0001_bs8_dp0.5_h4_s1l4 --train_model IRN_c_6_F_3_residual --evaluate False
```
Univariate, out 168
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 168 --pred_len 168 --hidden-size 4 --stacks 1 --levels 4 --lr 5e-5 --batch_size 8 --dropout 0.5 --model_name etth1_S_I720_O168_lr5e-5_bs8_dp0.5_h4_s1l4 --train_model IRN_c_6_F_3_residual --evaluate False
```
Univariate, out 336
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 7e-4 --batch_size 128 --dropout 0.5 --model_name etth1_S_I720_O336_lr1e-3_bs128_dp0.5_h1_s1l4 --train_model IRN_c_8_F_5_D_020 --evaluate False
```
Univariate, out 720
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 4 --stacks 1 --levels 5 --lr 1e-4 --batch_size 32 --dropout 0.5 --model_name etth1_S_I736_O720_lr1e-5_bs32_dp0.5_h4_s1l5 --train_model IRN_c_6_F_3_residual --evaluate False
```

#### For ETTH2 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 48 --label_len 24 --pred_len 24 --hidden-size 8 --stacks 1 --levels 3 --lr 0.007 --batch_size 16 --dropout 0.25 --model_name etth2_M_I48_O24_lr7e-3_bs16_dp0.25_h8_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 48
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 4 --lr 0.007 --batch_size 16 --dropout 0.5 --model_name etth2_M_I96_O48_lr7e-3_bs4_dp0.5_h4_s1l4 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 168
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 0.5 --stacks 1 --levels 4 --lr 5e-5 --batch_size 16 --dropout 0.5 --model_name etth2_M_I336_O168_lr5e-5_bs16_dp0.5_h0.5_s1l4 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 336
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 5e-5 --batch_size 128 --dropout 0.5 --model_name etth2_M_I336_O336_lr5e-5_bs128_dp0.5_h1_s1l4 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 720
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 4 --stacks 1 --levels 5 --lr 3e-5 --batch_size 128 --dropout 0.5 --model_name etth2_M_I736_O720_lr1e-5_bs64_dp0.5_h4_s1l5 --train_model IRN_c_8_F_5 --evaluate False
```
Univariate, out 24
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 48 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 3 --lr 0.001 --batch_size 16 --dropout 0 --model_name etth2_S_I48_O24_lr1e-3_bs16_dp0_h4_s1l3 --train_model IRN_c_8_F_5 --evaluate False
```
Univariate, out 48
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 2 --levels 4 --lr 0.0007 --batch_size 32 --dropout 0.5 --model_name etth2_S_I96_O48_lr1e-3_bs32_dp0.5_h4_s2l4 long --evaluate False
```
Univariate, out 168
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 2 --stacks 2 --levels 3 --lr 1e-4 --batch_size 8 --dropout 0.2 --model_name etth2_S_I336_O168_lr1e-4_bs8_dp0_h4_s1l3 --train_model IRN_c_8_F_5 --evaluate False
```
Univariate, out 336
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 8 --stacks 1 --levels 3 --lr 7e-4 --batch_size 512 --dropout 0.5 --model_name etth2_S_I336_O336_lr5e-4_bs512_dp0.5_h8_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```
Univariate, out 720
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 720 --label_len 720 --pred_len 720 --hidden-size 8 --stacks 1 --levels 3 --lr 1e-4 --batch_size 128 --dropout 0.6 --model_name etth2_S_I736_O720_lr1e-5_bs128_dp0.6_h8_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```

#### For ETTM1 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 48 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 3 --lr 0.005 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I48_O24_lr7e-3_bs16_dp0.25_h8_s1l3 --train_model IRN_c_6_F_3 --evaluate False
```
multivariate, out 48
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 2 --levels 4 --lr 0.001 --batch_size 16 --dropout 0.5 --model_name ettm1_M_I96_O48_lr1e-3_bs16_dp0.5_h4_s2l4 --train_model IRN_c_6_F_3_residual --evaluate False
```
multivariate, out 96
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 384 --label_len 96 --pred_len 96 --hidden-size 0.3 --stacks 2 --levels 4 --lr 5e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I384_O96_lr5e-5_bs32_dp0.5_h0.5_s2l4 --train_model IRN_c_8_F_5 --evaluate False
```
multivariate, out 288
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 672 --label_len 288 --pred_len 288 --hidden-size 4 --stacks 1 --levels 5 --lr 1e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I672_O288_lr1e-5_bs32_dp0.5_h0.5_s1l5 --train_model IRN_c_6_F_3_residual --evaluate False
```
multivariate, out 672
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 672 --label_len 672 --pred_len 672 --hidden-size 4 --stacks 2 --levels 5 --lr 2e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I672_O672_lr1e-5_bs32_dp0.5_h4_s2l5 --train_model IRN_c_8_F_5 --evaluate False
```
Univariate, out 24
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 96 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 4 --lr 0.001 --batch_size 8 --dropout 0.3 --model_name ettm1_S_I96_O24_lr1e-3_bs8_dp0_h4_s1l4 --train_model IRN_c_8_F_3 --evaluate False
```
Univariate, out 48
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 3 --lr 0.0005 --batch_size 16 --dropout 0.2 --model_name ettm1_S_I96_O48_lr5e-4_bs16_dp0_h4_s1l3 --train_model IRN_c_8_F_3 --evaluate False
```
Univariate, out 96
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 384 --label_len 96 --pred_len 96 --hidden-size 2 --stacks 1 --levels 4 --lr 1e-5 --batch_size 8 --dropout 0 --model_name ettm1_S_I384_O96_lr1e-5_bs8_dp0_h2_s1l4 --train_model IRN_c_6_F_3_residual --evaluate False
```
Univariate, out 288
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 384 --label_len 288 --pred_len 288 --hidden-size 4 --stacks 1 --levels 4 --lr 1e-5 --batch_size 64 --dropout 0 --model_name ettm1_S_I384_O288_lr1e-5_bs64_dp0_h4_s1l4 --train_model IRN_c_8_F_3 --evaluate False
```
Univariate, out 672
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 672 --label_len 672 --pred_len 672 --hidden-size 1 --stacks 1 --levels 5 --lr 1e-4 --batch_size 32 --model_name ettm1_S_I672_O672_lr1e-4_bs32_dp0.5_h1_s1l5i --train_model IRN_c_6_F_3 --evaluate False
```


##### ETT Parameter highlights

| Parameter Name | Description                  | Parameter in paper | Default                    |
| -------------- | ---------------------------- | ------------------ | -------------------------- |
| root_path      | The root path of subdatasets | N/A                | './datasets/ETT-data/ETT/' |
| data           | Subdataset                   | N/A                | ETTh1                      |
| pred_len       | Horizon                      | Horizon            | 48                         |
| seq_len        | Look-back window             | Look-back window   | 96                         |
| batch_size     | Batch size                   | batch size         | 32                         |
| lr             | Learning rate                | learning rate      | 0.0001                     |
| hidden-size    | hidden expansion             | h                  | 1                          |
| levels         | SCINet block levels          | L                  | 3                          |
| stacks         | The number of SCINet blocks  | K                  | 1                          |


#### For PEMS dataset:

pems03
```
python run_pems.py --dataset PEMS03 --hidden-size 0.0625 --dropout 0.25 --model_name pems03_h0.0625_dp0.25 --window_size 12 --train_model IRN_c_8_F_3 --evaluate False
```

pems04
```
python run_pems.py --dataset PEMS04 --hidden-size 0.1 --dropout 0.2 --model_name pems04_h0.0625_dp0 --window_size 12 --train_model IRN_c_8_F_3 --evaluate False
```

pems07
```
python run_pems.py --dataset PEMS07 --hidden-size 0.08 --dropout 0.25 --model_name pems07_h0.08_dp0.25 --window_size 24 --train_model IRN_c_8_F_3 --evaluate False
```

pems08
```
python run_pems.py --dataset PEMS08 --hidden-size 0.5 --dropout 0.25 --model_name pems08_h1_dp0.5 --window_size 12  --train_model IRN_c_8_F_5 --evaluate False
```

##### PEMS Parameter highlights

| Parameter Name | Description             | Parameter in paper | Default |
| -------------- | ----------------------- | ------------------ | ------- |
| dataset        | Name of dataset         | N/A                | PEMS08  |
| horizon        | Horizon                 | Horizon            | 12      |
| window_size    | Look-back window        | Look-back window   | 12      |
| hidden-size    | hidden expansion        | h                  | 1       |
| levels         | SCINet block levels     | L                  | 2       |
| stacks         | The number of SCINet block| K                | 1       |




#### For Exchange rate dataset:

predict 3 
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 3 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o3_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --train_model IRN_c_6_F_3 --evaluate False
```
predict 6
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 6 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o6_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --train_model IRN_c_6_F_3 --evaluate False
```
predict 12
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 12 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o12_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5_single_ex --epochs 150 --train_model IRN_c_6_F_3_D --evaluate False
```
predict 24
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 24 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 7e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o24_lr7e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --train_model IRN_c_6_F_3_residual --evaluate False
```


#### For Solar dataset:

predict 3 
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 3 --hidden-size 1  --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o3_lr1e-4_bs256_dp0.25_h1_s2l4_w0.5 --train_model IRN_c_6_F_3_residual --evaluate False
```
predict 6
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 6 --hidden-size 0.5 --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o6_lr1e-4_bs256_dp0.25_h0.5_s2l4_w0.5  --train_model IRN_c_8_F_3 --evaluate False
```
predict 12
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 12 --hidden-size 2 --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 812 --model_name so_I160_o12_lr1e-4_bs1024_dp0.25_h2_s2l4_w0.5  --train_model IRN_c_6_F_3 --evaluate False
```
predict 24
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 24 --hidden-size 2 --lastWeight 0.5 --stacks 1 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o24_lr1e-4_bs256_dp0.25_h1_s1l4_w0.5 --train_model IRN_c_6_F_3_D --evaluate False
```

#### For Traffic dataset (warning: 20,000MiB+ memory usage!):

predict 3 
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 3 --hidden-size 1 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.5 --batch_size 16 --model_name traf_I168_o3_lr5e-4_bs16_dp0.5_h1_s2l3_w1.0 --train_model IRN_c_8_F_3 --evaluate False
```
predict 6
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 6 --hidden-size 1 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.25 --batch_size 16 --model_name traf_I168_o6_lr5e-4_bs16_dp0.25_h2_s1l3_w1.0 --train_model IRN_c_8_F_3 --evaluate False
```
predict 12
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 12 --hidden-size 0.5 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.25 --batch_size 16 --model_name traf_I168_o12_lr5e-4_bs16_dp0.25_h0.5_s2l3_w1.0_short --train_model IRN_c_6_F_3 --evaluate False
```
predict 24
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 24 --hidden-size 1 --single_step 1 --stacks 2 --levels 2 --lr 5e-4 --dropout 0.5 --batch_size 16 --model_name traf_I168_o24_lr5e-4_bs16_dp0.5_h2_s2l2_w1.0  --train_model IRN_c_8_F_3 --evaluate False
```


#### For Electricity dataset:

predict 3
``` 
python run_financial.py --dataset_name electricity --window_size 168 --horizon 3 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o3_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --train_model IRN_c_8_F_5 --evaluate False
```
predict 6
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 6 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o6_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --train_model IRN_c_8_F_3 --evaluate False
```
predict 12
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 12 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o12_lr9e-3_bs32_dp0_h8_s2l3_w0.5_just_gr --groups 321 --train_model IRN_c_4_F_3 --evaluate False
```
predict 24
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 24 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o24_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --train_model IRN_c_8_F_5 --evaluate False
```



##### Exchange, Solar, Traffic, and Electricity Parameter highlights

| Parameter Name | Description               | Parameter in paper      | Default                                |
| -------------- | ------------------------- | ----------------------- | -------------------------------------- |
| dataset_name   | Data name                 | N/A                     | exchange_rate                          |
| horizon        | Horizon                   | Horizon                 | 3                                      |
| window_size    | Look-back window          | Look-back window        | 168                                    |
| batch_size     | Batch size                | batch size              | 8                                      |
| lr             | Learning rate             | learning rate           | 5e-3                                   |
| hidden-size    | hidden expansion          | h                       | 1                                      |
| levels         | SCINet block levels       | L                       | 3                                      |
| stacks         | The number of SCINet block| K                       | 1                                      |
| lastweight     | Loss weight of the last frame| Loss weight ($\lambda$) | 1.0                                 |

## Run Pretrain testing code


### (Very Important)Precautions for testing pretrain models

All pretrain models were trained using 8 GPUs and these are assigned differently for each parameter. Therefore, we recommand using 8 GPUs to prevent errors.
GPU setting command is as below.
```
export CUDA_VISIBLE_DEVICES=0,1,2,3,4,5,6,7
```

#### For ETTH1 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 168 --label_len 24 --pred_len 24 --hidden-size 0.5 --stacks 1 --levels 3 --lr 1e-3 --batch_size 64 --dropout 0.5 --model_name etth1_M_I48_O24_lr3e-3_bs8_dp0.5_h4_s1l3 --pretrain_path ./checkpoints/ETTh1/multi/seq24/bestmodel.pth --evaluate True
```
multivariate, out 48
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 3 --lr 0.003 --batch_size 16 --dropout 0.25 --model_name etth1_M_I96_O48_lr0.009_bs16_dp0.25_h4_s1l --pretrain_path ./checkpoints/ETTh1/multi/seq48/bestmodel.pth --evaluate True
```
multivariate, out 168
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 4 --stacks 1 --levels 3 --lr 5e-4 --batch_size 32 --dropout 0.5 --model_name etth1_M_I336_O168_lr5e-4_bs32_dp0.5_h4_s1l3 --pretrain_path ./checkpoints/ETTh1/multi/seq168/bestmodel.pth --evaluate True
```
multivariate, out 336
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 6e-4 --batch_size 512 --dropout 0.5 --model_name etth1_M_I336_O336_lr1e-4_bs512_dp0.5_h1_s1l4 --pretrain_path ./checkpoints/ETTh1/multi/seq336/bestmodel.pth --evaluate True
```
multivariate, out 720
```
python run_ETTh.py --data ETTh1 --features M  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 1 --stacks 1 --levels 5 --lr 5e-5 --batch_size 64 --dropout 0.5 --model_name etth1_M_I736_O720_lr5e-5_bs256_dp0.5_h1_s1l5 --pretrain_path ./checkpoints/ETTh1/multi/seq720/bestmodel.pth --evaluate True
```
Univariate, out 24
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 64 --label_len 24 --pred_len 24 --hidden-size 8 --stacks 1 --levels 3 --lr 0.007 --batch_size 64 --dropout 0.26 --model_name etth1_S_I64_O24_lr0.007_bs64_dp0.25_h8_s1l3 --pretrain_path ./checkpoints/ETTh1/single/seq24/bestmodel.pth --evaluate True
```
Univariate, out 48
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 4 --lr 0.0001 --batch_size 8 --dropout 0.5 --model_name etth1_S_I720_O48_lr0.0001_bs8_dp0.5_h4_s1l4 --pretrain_path ./checkpoints/ETTh1/single/seq48/bestmodel.pth --evaluate True
```
Univariate, out 168
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 168 --pred_len 168 --hidden-size 4 --stacks 1 --levels 4 --lr 5e-5 --batch_size 8 --dropout 0.5 --model_name etth1_S_I720_O168_lr5e-5_bs8_dp0.5_h4_s1l4 --pretrain_path ./checkpoints/ETTh1/single/seq168/bestmodel.pth --evaluate True
```
Univariate, out 336
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 720 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 7e-4 --batch_size 128 --dropout 0.5 --model_name etth1_S_I720_O336_lr1e-3_bs128_dp0.5_h1_s1l4 --pretrain_path ./checkpoints/ETTh1/single/seq336/bestmodel.pth --evaluate True
```
Univariate, out 720
```
python run_ETTh.py --data ETTh1 --features S  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 4 --stacks 1 --levels 5 --lr 1e-4 --batch_size 32 --dropout 0.5 --model_name etth1_S_I736_O720_lr1e-5_bs32_dp0.5_h4_s1l5 --pretrain_path ./checkpoints/ETTh1/single/seq720/bestmodel.pth --evaluate True
```

#### For ETTH2 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 48 --label_len 24 --pred_len 24 --hidden-size 8 --stacks 1 --levels 3 --lr 0.007 --batch_size 16 --dropout 0.25 --model_name etth2_M_I48_O24_lr7e-3_bs16_dp0.25_h8_s1l3 --pretrain_path ./checkpoints/ETTh2/multi/seq24/bestmodel.pth --evaluate True
```
multivariate, out 48
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 4 --lr 0.007 --batch_size 16 --dropout 0.5 --model_name etth2_M_I96_O48_lr7e-3_bs4_dp0.5_h4_s1l4 --pretrain_path ./checkpoints/ETTh2/multi/seq48/bestmodel.pth --evaluate True
```
multivariate, out 168
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 0.5 --stacks 1 --levels 4 --lr 5e-5 --batch_size 16 --dropout 0.5 --model_name etth2_M_I336_O168_lr5e-5_bs16_dp0.5_h0.5_s1l4 --pretrain_path ./checkpoints/ETTh2/multi/seq168/bestmodel.pth --evaluate True
```
multivariate, out 336
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 1 --stacks 1 --levels 4 --lr 5e-5 --batch_size 128 --dropout 0.5 --model_name etth2_M_I336_O336_lr5e-5_bs128_dp0.5_h1_s1l4 --pretrain_path ./checkpoints/ETTh2/multi/seq336/bestmodel.pth --evaluate True
```
multivariate, out 720
```
python run_ETTh.py --data ETTh2 --features M  --seq_len 736 --label_len 720 --pred_len 720 --hidden-size 4 --stacks 1 --levels 5 --lr 3e-5 --batch_size 128 --dropout 0.5 --model_name etth2_M_I736_O720_lr1e-5_bs64_dp0.5_h4_s1l5 --pretrain_path ./checkpoints/ETTh2/multi/seq720/bestmodel.pth --evaluate True
```
Univariate, out 24
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 96 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 4 --lr 0.001 --batch_size 8 --dropout 0.3 --model_name ettm1_S_I96_O24_lr1e-3_bs8_dp0_h4_s1l4 --pretrain_path ./checkpoints/ETTh2/single/seq24/bestmodel.pth --evaluate True
```
Univariate, out 48
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 2 --levels 4 --lr 0.0007 --batch_size 32 --dropout 0.5 --model_name etth2_S_I96_O48_lr1e-3_bs32_dp0.5_h4_s2l4 --pretrain_path ./checkpoints/ETTh2/single/seq48/bestmodel.pth --evaluate True
```
Univariate, out 168
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 336 --label_len 168 --pred_len 168 --hidden-size 2 --stacks 2 --levels 3 --lr 1e-4 --batch_size 8 --dropout 0.2 --model_name etth2_S_I336_O168_lr1e-4_bs8_dp0_h4_s1l3 --pretrain_path ./checkpoints/ETTh2/single/seq168/bestmodel.pth --evaluate True
```
Univariate, out 336
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 336 --label_len 336 --pred_len 336 --hidden-size 8 --stacks 1 --levels 3 --lr 7e-4 --batch_size 512 --dropout 0.5 --model_name etth2_S_I336_O336_lr5e-4_bs512_dp0.5_h8_s1l3 --pretrain_path ./checkpoints/ETTh2/single/seq336/bestmodel.pth --evaluate True
```
Univariate, out 720
```
python run_ETTh.py --data ETTh2 --features S  --seq_len 720 --label_len 720 --pred_len 720 --hidden-size 8 --stacks 1 --levels 3 --lr 1e-4 --batch_size 128 --dropout 0.6 --model_name etth2_S_I736_O720_lr1e-5_bs128_dp0.6_h8_s1l3 --pretrain_path ./checkpoints/ETTh2/single/seq720/bestmodel.pth --evaluate True
```

#### For ETTM1 dataset:

multivariate, out 24
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 48 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 3 --lr 0.005 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I48_O24_lr7e-3_bs16_dp0.25_h8_s1l3 --pretrain_path ./checkpoints/ETTm1/multi/seq24/bestmodel.pth --evaluate True
```
multivariate, out 48
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 2 --levels 4 --lr 0.001 --batch_size 16 --dropout 0.5 --model_name ettm1_M_I96_O48_lr1e-3_bs16_dp0.5_h4_s2l4 --pretrain_path ./checkpoints/ETTm1/multi/seq48/bestmodel.pth --evaluate True
```
multivariate, out 96
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 384 --label_len 96 --pred_len 96 --hidden-size 0.3 --stacks 2 --levels 4 --lr 5e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I384_O96_lr5e-5_bs32_dp0.5_h0.5_s2l4 --pretrain_path ./checkpoints/ETTm1/multi/seq96/bestmodel.pth --evaluate True
```
multivariate, out 288
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 672 --label_len 288 --pred_len 288 --hidden-size 4 --stacks 1 --levels 5 --lr 1e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I672_O288_lr1e-5_bs32_dp0.5_h0.5_s1l5 --pretrain_path ./checkpoints/ETTm1/multi/seq288/bestmodel.pth --evaluate True
```
multivariate, out 672
```
python run_ETTh.py --data ETTm1 --features M  --seq_len 672 --label_len 672 --pred_len 672 --hidden-size 4 --stacks 2 --levels 5 --lr 2e-5 --batch_size 32 --dropout 0.5 --model_name ettm1_M_I672_O672_lr1e-5_bs32_dp0.5_h4_s2l5 --pretrain_path ./checkpoints/ETTm1/multi/seq672/bestmodel.pth --evaluate True
```
Univariate, out 24
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 96 --label_len 24 --pred_len 24 --hidden-size 4 --stacks 1 --levels 4 --lr 0.001 --batch_size 8 --dropout 0.3 --model_name ettm1_S_I96_O24_lr1e-3_bs8_dp0_h4_s1l4 --pretrain_path ./checkpoints/ETTm1/single/seq24/bestmodel.pth --evaluate True
```
Univariate, out 48
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 96 --label_len 48 --pred_len 48 --hidden-size 4 --stacks 1 --levels 3 --lr 0.0005 --batch_size 16 --dropout 0.2 --model_name ettm1_S_I96_O48_lr5e-4_bs16_dp0_h4_s1l3 --pretrain_path ./checkpoints/ETTm1/single/seq48/bestmodel.pth --evaluate True
```
Univariate, out 96
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 384 --label_len 96 --pred_len 96 --hidden-size 2 --stacks 1 --levels 4 --lr 1e-5 --batch_size 8 --dropout 0 --model_name ettm1_S_I384_O96_lr1e-5_bs8_dp0_h2_s1l4 --pretrain_path ./checkpoints/ETTm1/single/seq96/bestmodel.pth --evaluate True
```
Univariate, out 288
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 384 --label_len 288 --pred_len 288 --hidden-size 4 --stacks 1 --levels 4 --lr 1e-5 --batch_size 64 --dropout 0 --model_name ettm1_S_I384_O288_lr1e-5_bs64_dp0_h4_s1l4 --pretrain_path ./checkpoints/ETTm1/single/seq288/bestmodel.pth --evaluate True
```
Univariate, out 672
```
python run_ETTh.py --data ETTm1 --features S  --seq_len 672 --label_len 672 --pred_len 672 --hidden-size 1 --stacks 1 --levels 5 --lr 1e-4 --batch_size 32 --model_name ettm1_S_I672_O672_lr1e-4_bs32_dp0.5_h1_s1l5i --pretrain_path ./checkpoints/ETTm1/single/seq672/bestmodel.pth --evaluate True
```


##### ETT Parameter highlights

| Parameter Name | Description                  | Parameter in paper | Default                    |
| -------------- | ---------------------------- | ------------------ | -------------------------- |
| root_path      | The root path of subdatasets | N/A                | './datasets/ETT-data/ETT/' |
| data           | Subdataset                   | N/A                | ETTh1                      |
| pred_len       | Horizon                      | Horizon            | 48                         |
| seq_len        | Look-back window             | Look-back window   | 96                         |
| batch_size     | Batch size                   | batch size         | 32                         |
| lr             | Learning rate                | learning rate      | 0.0001                     |
| hidden-size    | hidden expansion             | h                  | 1                          |
| levels         | SCINet block levels          | L                  | 3                          |
| stacks         | The number of SCINet blocks  | K                  | 1                          |


#### For PEMS dataset:

pems03
```
python run_pems.py --dataset PEMS03 --hidden-size 0.0625 --dropout 0.25 --model_name pems03_h0.0625_dp0.25 --pretrain_path ./checkpoints/PEMS/03/bestmodel.pth --evaluate True
```

pems04
```
python run_pems.py --dataset PEMS04 --hidden-size 0.1 --dropout 0.2 --model_name pems04_h0.0625_dp0 --pretrain_path ./checkpoints/PEMS/04/bestmodel.pth --evaluate True
```

pems07
```
python run_pems.py --dataset PEMS07 --hidden-size 0.08 --dropout 0.25 --window_size 24 --model_name pems07_h0.08_dp0.25 --pretrain_path ./checkpoints/PEMS/07/bestmodel.pth --evaluate True
```

pems08
```
python run_pems.py --dataset PEMS08 --hidden-size 0.5 --dropout 0.25 --model_name pems08_h1_dp0.5 --model_name pems07_h0.08_dp0.25 --pretrain_path ./checkpoints/PEMS/08/bestmodel.pth
```

##### PEMS Parameter highlights

| Parameter Name | Description             | Parameter in paper | Default |
| -------------- | ----------------------- | ------------------ | ------- |
| dataset        | Name of dataset         | N/A                | PEMS08  |
| horizon        | Horizon                 | Horizon            | 12      |
| window_size    | Look-back window        | Look-back window   | 12      |
| hidden-size    | hidden expansion        | h                  | 1       |
| levels         | SCINet block levels     | L                  | 2       |
| stacks         | The number of SCINet block| K                | 1       |




#### For Exchange rate dataset:

predict 3 
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 3 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o3_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --pretrain_path ./checkpoints/exchange/seq3/bestmodel.pth --evaluate True
```
predict 6
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 6 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o6_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --pretrain_path ./checkpoints/exchange/seq6/bestmodel.pth --evaluate True
```
predict 12
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 12 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 5e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o12_lr5e-3_bs4_dp0.5_h0.125_s1l3_w0.5_single_ex --epochs 150 --pretrain_path ./checkpoints/exchange/seq12/bestmodel.pth --evaluate True
```
predict 24
```
python run_financial.py --dataset_name exchange_rate --window_size 168 --horizon 24 --hidden-size 0.125 --lastWeight 0.5 --stacks 1 --levels 3 --lr 7e-3 --dropout 0.5 --batch_size 4 --model_name ex_I168_o24_lr7e-3_bs4_dp0.5_h0.125_s1l3_w0.5 --epochs 150 --pretrain_path ./checkpoints/exchange/seq24/bestmodel.pth --evaluate True
```


#### For Solar dataset:

predict 3 
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 3 --hidden-size 1  --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o3_lr1e-4_bs256_dp0.25_h1_s2l4_w0.5 --pretrain_path ./checkpoints/solar/seq3/bestmodel.pth --evaluate True
```
predict 6
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 6 --hidden-size 0.5 --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o6_lr1e-4_bs256_dp0.25_h0.5_s2l4_w0.5  --pretrain_path ./checkpoints/solar/seq6/bestmodel.pth --evaluate True
```
predict 12
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 12 --hidden-size 2 --lastWeight 0.5 --stacks 2 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 812 --model_name so_I160_o12_lr1e-4_bs1024_dp0.25_h2_s2l4_w0.5  --pretrain_path ./checkpoints/solar/seq12/bestmodel.pth --evaluate True
```
predict 24
```
python run_financial.py --dataset_name solar_AL --window_size 160 --horizon 24 --hidden-size 2 --lastWeight 0.5 --stacks 1 --levels 4 --lradj 2 --lr 1e-4 --dropout 0.25 --batch_size 256 --model_name so_I160_o24_lr1e-4_bs256_dp0.25_h1_s1l4_w0.5 --pretrain_path ./checkpoints/solar/seq24/bestmodel.pth --evaluate True
```

#### For Traffic dataset (warning: 20,000MiB+ memory usage!):

predict 3 
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 3 --hidden-size 1 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.5 --batch_size 16 --model_name traf_I168_o3_lr5e-4_bs16_dp0.5_h1_s2l3_w1.0 --pretrain_path ./checkpoints/traffic/seq3/bestmodel.pth --evaluate True
```
predict 6
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 6 --hidden-size 1 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.25 --batch_size 16 --model_name traf_I168_o6_lr5e-4_bs16_dp0.25_h2_s1l3_w1.0 --pretrain_path ./checkpoints/traffic/seq6/bestmodel.pth --evaluate True
```
predict 12
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 12 --hidden-size 0.5 --single_step 1 --stacks 2 --levels 3 --lr 5e-4 --dropout 0.25 --batch_size 16 --model_name traf_I168_o12_lr5e-4_bs16_dp0.25_h0.5_s2l3_w1.0_short --pretrain_path ./checkpoints/traffic/seq12/bestmodel.pth --evaluate True
```
predict 24
```
python run_financial.py --dataset_name traffic --window_size 168 --horizon 24 --hidden-size 1 --single_step 1 --stacks 2 --levels 2 --lr 5e-4 --dropout 0.5 --batch_size 16 --model_name traf_I168_o24_lr5e-4_bs16_dp0.5_h2_s2l2_w1.0  --pretrain_path ./checkpoints/traffic/seq24/bestmodel.pth --evaluate True
```


#### For Electricity dataset:

predict 3
``` 
python run_financial.py --dataset_name electricity --window_size 168 --horizon 3 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o3_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --pretrain_path ./checkpoints/electricity/seq3/bestmodel.pth --evaluate True
```
predict 6
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 6 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o6_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --pretrain_path ./checkpoints/electricity/seq6/bestmodel.pth --evaluate True
```
predict 12
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 12 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o12_lr9e-3_bs32_dp0_h8_s2l3_w0.5_just_gr --groups 321 --pretrain_path ./checkpoints/electricity/seq12/bestmodel.pth --evaluate True
```
predict 24
```
python run_financial.py --dataset_name electricity --window_size 168 --horizon 24 --hidden-size 8 --single_step 1 --stacks 2 --levels 3 --lr 9e-3 --dropout 0 --batch_size 32 --model_name ele_I168_o24_lr9e-3_bs32_dp0_h8_s2l3_w0.5 --groups 321 --pretrain_path ./checkpoints/electricity/seq24/bestmodel.pth --evaluate True
```



##### Exchange, Solar, Traffic, and Electricity Parameter highlights

| Parameter Name | Description               | Parameter in paper      | Default                                |
| -------------- | ------------------------- | ----------------------- | -------------------------------------- |
| dataset_name   | Data name                 | N/A                     | exchange_rate                          |
| horizon        | Horizon                   | Horizon                 | 3                                      |
| window_size    | Look-back window          | Look-back window        | 168                                    |
| batch_size     | Batch size                | batch size              | 8                                      |
| lr             | Learning rate             | learning rate           | 5e-3                                   |
| hidden-size    | hidden expansion          | h                       | 1                                      |
| levels         | SCINet block levels       | L                       | 3                                      |
| stacks         | The number of SCINet block| K                       | 1                                      |
| lastweight     | Loss weight of the last frame| Loss weight ($\lambda$) | 1.0                                 |