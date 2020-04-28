# Non Parallel Voice conversion using CycleGan-VC2

Converting voice from source to target speaker using a non-parallel dataset and cyclegan-vc2 architecture

## Datasets Used

- VCC 2016 
- Malayalam Dataset from openslr
- CMU Arctic (Indian accented english and US english)

## Usage

### Preprocess dataset for Training

Preprocess the wav files and store it in numpy format
For example, if the source is `SF1` and target is `TF1`\
(or can change the defaults inside prepocess_training.py and run it without any arguments)
```
$ python prepocess_training.py --train_A_dir ../data/vcc2016_training/SF1
                                --train_B_dir ../data/vcc2016_training/TF1
                                --cache_folder ../cache/
```
### Training

If the source is `SF1` and target is `TF1`
```
$ python train.py --logf0s_normalization ../cache/logf0s_normalization.npz --mcep_normalization ../cache/mcep_normalization.npz --coded_sps_A_norm coded_sps_A_norm --coded_sps_B_norm coded_sps_B_norm --resume_training_at ../cache/model_checkpoint/_CycleGAN_CheckPoint --validation_A_dir ../data/vcc2016_training/evaluation_all/SF1/ --output_A_dir ../data/vcc2016_training/converted_sound/SF1 --validation_B_dir ../data/vcc2016_training/evaluation_all/TF1/ --output_B_dir ../data/vcc2016_training/converted_sound/TF1/

```
### Test/Validating

For example, to test for voice conversion between `SF1` and `TF1`:
```
$python test.py --logf0s_normalization ../cache/logf0s_normalization.npz --mcep_normalization ../cache/mcep_normalization.npz --test_A_dir ../data/vcc2016_training/evaluation_all/SF1/ --output_A_dir ../data/vcc2016_training/converted_sound/SF1 --model_checkpoint ./model/_CycleGAN_CheckPoint
```