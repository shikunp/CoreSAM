# CoreSAM

Boosting SAM via intermediate-layer aggregation and cascade decoding for prompt-free core instance segmentation and RQD analysis

## Installation


### Main environment

| Component | Version |
| --- | --- |
| Python | 3.10 |
| PyTorch | 2.1.2 |
| Torchvision | 0.16.2 |
| MMCV with CUDA operators | 2.1.0 |
| MMEngine | 0.10.5 |
| MMDetection | 3.2.0 |
| MMPretrain | 1.1.1 |
| Transformers | 4.38.1 |
| PEFT | 0.8.2 |


## Dataset

| Resource | Download | Access code |
| --- | --- | --- |
| EX-Core images | [Kaggle](https://www.kaggle.com/datasets/feiyueliu/rqd-core-photo) | — |
| EX-Core images and annotations | [Baidu Netdisk](https://pan.baidu.com/s/1At6Kk4xMsK5cg_AYv8pumw?pwd=uh99) | `uh99` |

Arrange the annotated dataset in COCO format using the layout expected by the supplied configuration. The COCO category name is `core`. Preserve the image filenames and the train/validation/test split supplied with the annotated dataset.

```text
CoreSAM/
├── configs/
│   └── sam_cascademaskrcnn_peft_r-16_huge.py
├── data/
│   └── Corenew/
│       ├── annotations/
│       │   ├── instances_train2017.json
│       │   ├── instances_val2017.json
│       │   └── instances_test2017.json
│       ├── train2017/
│       ├── val2017/
│       └── test2017/
├── mmdet/
│   └── coresam/
├── mmpretrain/
├── demo/
└── tools/
```

The default dataset root is `data/Corenew/`. For a different location, update `data_root` in the configuration before running the commands below.

## Model resources

### SAM-H initialization

Download the Hugging Face SAM-H configuration and pretrained parameters into the directory used by the configuration.

```bash
python -c "from huggingface_hub import snapshot_download; snapshot_download(repo_id='facebook/sam-vit-huge', local_dir='work_dirs/sam_cache/sam_vit_huge', allow_patterns=['config.json', 'pytorch_model.bin'])"
```

The resulting directory must contain `config.json` and `pytorch_model.bin`. The encoder constructor uses these resources for training, evaluation, and image inference. [SAM-H model files](https://huggingface.co/facebook/sam-vit-huge/tree/main)

### CoreSAM-H trained checkpoint

| Checkpoint | Download | Access code |
| --- | --- | --- |
| `CoreSAM-H_best_coco_segm_mAP.pth` | [Baidu Netdisk](https://pan.baidu.com/s/1tcSJ3tqe9pKghnpCO1-YgA?pwd=91ef) | `91ef` |



## License

CoreSAM code is distributed under Apache-2.0. Upstream copyright statements and license texts are retained in this repository. Data and downloaded model resources are subject to their respective providers' terms. [License](LICENSE), [third-party notices](NOTICE), [upstream license copies](licenses/)
