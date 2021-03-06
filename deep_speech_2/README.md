# Deep Speech 2 on PaddlePaddle

## Installation

Please replace `$PADDLE_INSTALL_DIR` with your own paddle installation directory.

```
sh setup.sh
export LD_LIBRARY_PATH=$PADDLE_INSTALL_DIR/Paddle/third_party/install/warpctc/lib:$LD_LIBRARY_PATH
```

For some machines, we also need to install libsndfile1. Details to be added.

## Usage

### Preparing Data

```
cd datasets
sh run_all.sh
cd ..
```

`sh run_all.sh` prepares all ASR datasets (currently, only LibriSpeech available). After running, we have several summarization manifest files in json-format.

A manifest file summarizes a speech data set, with each line containing the meta data (i.e. audio filepath, transcript text, audio duration) of each audio file within the data set, in json format. Manifest file serves as an interface informing our system of  where and what to read the speech samples.


More help for arguments:

```
python datasets/librispeech/librispeech.py --help
```

### Preparing for Training

```
python compute_mean_std.py
```

`python compute_mean_std.py` computes mean and stdandard deviation for audio features, and save them to a file with a default name `./mean_std.npz`. This file will be used in both training and inferencing.

More help for arguments:

```
python compute_mean_std.py --help
```

### Training

For GPU Training:

```
CUDA_VISIBLE_DEVICES=0,1,2,3,4,5,6,7 python train.py
```

For CPU Training:

```
python train.py --use_gpu False
```

More help for arguments:

```
python train.py --help
```

### Inferencing

```
CUDA_VISIBLE_DEVICES=0 python infer.py
```

More help for arguments:

```
python infer.py --help
```

### Evaluating

```
CUDA_VISIBLE_DEVICES=0 python evaluate.py
```

More help for arguments:

```
python evaluate.py --help
```

### Parameters tuning

Parameters tuning for the CTC beam search decoder

```
CUDA_VISIBLE_DEVICES=0 python tune.py
```

More help for arguments:

```
python tune.py --help
```
