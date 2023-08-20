# SwinJSCC: Taming Swin Transformer for Joint Source-Channel Coding

This paper has been partially presented in IEEE ICASSP 2023 "[WITT: A Wireless Image Transmission Transformer For Semantic Communications](https://arxiv.org/abs/2211.00937)" and the code is available at [_](https://github.com/KeYang8/WITT).

## Introduction
In this paper, we establish a more expressive JSCC codec architecture that can also adapt flexibly to diverse channel states and transmission rates within a single model. Specifically, we demonstrate that with elaborate design, neural JSCC codec built on the emerging Swin Transformer backbone can achieve superior performance than conventional neural JSCC codecs built upon CNN while also requiring lower end-to-end processing latency. Paired with two well-designed spatial modulation modules that scale latent representations based on the channel state information and target transmission rate, our baseline SwinJSCC can further upgrade to a versatile version, which increases its capability to adapt to diverse channel conditions and rate configurations. Extensive experimental results show that our SwinJSCC achieves better or comparable performance versus the state-of-the-art engineered BPG + 5G LDPC coded transmission system with much faster end-to-end coding speed, especially for high-resolution images, in which case traditional CNN-based JSCC yet falls behind due to its limited model capacity. 
![ ](overview.png)
>  The overall architecture of the proposed SwinJSCC scheme for wireless image transmission.


## Experimental results

* we employ the BPG codec for compression combined with 5G LDPC codes for channel coding (marked as “BPG + LDPC”). Here, we considered 5G LDPC codes with a block length of 6144 bits for different coding rates and quadrature amplitude modulations (QAM). 
* the ideal capacity-achieving channel code is also considered during evaluation (marked as “BPG + Capacity”).


# Installation
We implement WITT under python 3.8 and PyTorch 1.9. 


# Usage

## Test
All pretrain models can be found in [Aliyun drive](https://www.aliyundrive.com/s/AFu5fZMjgCL(password:p5ip))(password:p5ip) or [Google drive](https://drive.google.com/drive/folders/1_EouRY4yYvMCtamX2ReBzEd5YBQbyesc?usp=drive_link)

```
python test.py --trainset {'CIFAR10', 'DIV2K'} --testset {'CIFAR10', 'kodak', 'CLIC21'} -- distortion-metric {'MSE', 'MS-SSIM'} --model {'SwinJSCC_w/o_SAandRA', 'SwinJSCC_w/_SA', 'SwinJSCC_w/_RA', 'SwinJSCC_w/_SAandRA'} --channel-type {'awgn', 'rayleigh'} --C {bottleneck dimension} --multiple-snr {random or fixed snr} --model-size {'small', 'base', 'large'}
```

### For SwinJSCC w/ SA&RA model 

*e.g. C = [32, 64, 96, 128, 192], snr = [1, 4, 7, 10, 13], metric = PSNR, channel = AWGN

```
e.g.
python test.py --trainset DIV2K --testset kodak -- distortion_metric MSE --model SwinJSCC_w/_SAandRA --channel_type awgn --C 32,64,96,128,192 -- multiple-snr 1,4,7,10,13 --model-size base
```

You can apply our method on your own images.


# Acknowledgement
The implementation is based on [WITT: A Wireless Image Transmission Transformer For Semantic Communications](https://arxiv.org/abs/2211.00937) and [Swin Transformer](https://github.com/microsoft/Swin-Transformer).

# Related links
* BPG image format by _Fabrice Bellard_: https://bellard.org/bpg
* Sionna An Open-Source Library for Next-Generation Physical Layer Research: https://github.com/NVlabs/sionna
* DIV2K image dataset: https://data.vision.ee.ethz.ch/cvl/DIV2K/
* Kodak image dataset: http://r0k.us/graphics/kodak/
* CLIC image dataset:  http://compression.cc
