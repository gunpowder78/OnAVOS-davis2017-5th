Code for OnAVOS

Requires a good GPU with at least 11GB memory (e.g. 1080 TI or TITAN X)

Instructions for running:
1) install tensorflow and possibly other required libraries using pip
2) download the models and put them in OnAVOS/models/
3) choose a config you want to run from configs/
I recommend to start with configs/DAVIS16_oneshot (which does the one-shot approach without adaptation on DAVIS 2016)
4) change the data directori(es) in the first lines of the config to your DAVIS path
5) run "python main.py configs/DAVIS16_oneshot" (or a different config)

Additional instructions for DAVIS2017:
1) download the lucid data and change the path in configs/DAVIS17_online to point to it
2) copy the txt files from OnAVOS/ImageSets2017_with_ids/ to the ImageSets folder of your DAVIS 2017 data
3) follow instructions from above using the configs/DAVIS17_online config

Instructions for running on a custom dataset (note that this is based on the implementation for DAVIS2017, so that your dataset needs to be converted to the folder structure - an alternative is to write custom code to load your dataset):
1) download the pascal or pascal_up model and put them in OnAVOS/models/
2) choose a config you want to run from configs/ 
I recommend to start with configs/custom_oneshot The custom_up_oneshot adds upsampling layers, which might improve the accuracy, but will increase runtime memory consumption. If you want to add online adaptation, please compare to the online configs for DAVIS2016
3) Put your dataset in OnAVOS/custom_dataset while retaining the folder structure of the example images. The structure has to be the same as DAVIS 2017
4) run "python main.py configs/custom_oneshot" (or custom_up_oneshot)

Explanation of the most important config parameters:
n_finetune_steps: the number of steps for fine-tuning on the first frame
learning_rates: dictionary mapping from step number to a learning rate
n_adaptation_steps: number of update steps per frame during adaptation
adaptation_interval: during online adaptation, each adaptation_interval steps, the current frame is used for updating, otherwise the first frame
adaptation_learning_rate: learning rate used during online adaptation
posterior_positive_threshold: posterior probability threshold used to obtain the positive training examples
distance_negative_threshold: distance threshold (to the last mask) used to select the negative examples
adaptation_loss_scale: weighting factor of loss during online adaptation
adaptation_erosion_size: erosion size used during online adaptation (use 1 to disable erosion)
n_test_samples: the number of random sampled augmented versions of the input image per frame used during testing. Reduce this, to make inference much faster at the cost of a little bit accuracy

Outputs:
Log files will be stored in logs/
The results will be stored in forwarded/

Note that the code slightly changed since we wrote the paper and that randomness is involved, so the results you obtain might be different from the results reported in the paper. 
If the results differ significantly, please let me know.

If you need additional config or model files or have questions, please write me a mail: voigtlaender@vision.rwth-aachen.de

If you find this code useful, please consider citing
Paul Voigtlaender and Bastian Leibe: Online Adaptation of Convolutional Neural Networks for Video Object Segmentation, BMVC 2017
Paul Voigtlaender and Bastian Leibe: Online Adaptation of Convolutional Neural Networks for the 2017 DAVIS Challenge on Video Object Segmentation, The 2017 DAVIS Challenge on Video Object Segmentation - CVPR Workshops
