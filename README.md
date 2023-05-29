## Confidence-Geotagging Model 
### Current Scores
Confidence-based geotagging model has achived the following results:
- Median Average Error (Haversine Distance) of 4.97km
- Mean Average Error (Haversine Distance) of 541.92km 

### Training
To train your model, follow the instructions in `training.ipynb` or run it with `train.py` in the terminal:
```bash
python train.py --data_dir <data_path> --save_prefix <model_path> --arch char_lstm --split_uids
--batch_size 128 --loss l1 --optimizer adamw --scheduler constant --lr 5e-4 --num_epoch 10 
--conf_estim --confidence_validation_criterion
```

All arguments can be seen in [aux_files/args_parser.py](./aux_files/args_parser.py)

#### Dependencies
```
pytorch == 1.7.1
numpy == 1.19.2
scikit-learn == 0.22.2
tqdm == 4.62.3
pandas == 1.0.3
```

### Custom Data 
To upload a custom dataset, you will need to implement a Dataloader in [data_loading.py](./data_loading.py). This Dataloader must return a `list of texts, a list of coordinates [longitude, latitude]`. Then, add the result to the `get_dataset` method in [aux_files/args_parser.py](./aux_files/args_parser.py), and you'll be able to select it with the `dataset_name` argument.

For relevant data sets, please check the Existing Challenges section

### Confidence
To use confidence estimation, set the `conf_estim` and `confidence_validation_criterion` arguments to True. You can set the array to `model_save_band` to show the top predictions by `confidence_bands` (as a percentage from 0 to 100).
Use `model_save_band` to save the model by the best metric value for the selected band.

### Prediction 
An example of using the trained model is in [prediction.ipynb](./prediction.ipynb)

## Existing Challenges and Suggested Data Sets
### Regions Challenge 

The first suggested methodology (Challenge 1) on training the model is to look into the dataset of top most populated regions around the world.

The provided dataset is **[here](https://drive.google.com/file/d/1thkE-hgT3sDtZqILZH17Hyayy0hkk_jh/view?usp=share_link)**, which:

- is an annotated corpus of 500k texts, as well as the respective geocoordinates
- covers 123 regions
- includes 5000 tweets per location

### Seasons Сhallenge

Challenge 2 sets the goal to identify the correlation between the time/date of post, the content, and the location. 

Time zone differences, as well as seasonality of the events, should be analyzed and used to predict the location. For example: snow is more likely to appear in the Northern Hemisphere, especially if in December. Rock concerts are more likely to happen in the evening and in bigger cities, so the time of the post about a concert should be used to identify the time zone of the author and narrow down the list of potential locations.


The provided dataset is **[here](https://drive.google.com/drive/folders/1P2QUGFBKaqdpZ4xAHmJMe2I57I94MJyO?usp=sharing)**, which:
- is a .json of >600.000 texts 
- collected over the span of 12 months
- covers 15 different time zones 
- focuses on 6 countries (Cuba, Iran, Russia, North Korea, Syria, Venezuela)

## Resources
### Contact 

If you would like to contact us with any questions, concerns, or feedback, help@yachay.ai is our email.

You also can check out our site, [yachay.ai](https://www.yachay.ai/), or any of our socials below.

<a href="https://discord.gg/msWFtcfmwe"><img src="https://cdn-icons-png.flaticon.com/512/3670/3670157.png" width=5% height=5%></img></a>     <a href="https://twitter.com/YachayAi"><img src="https://cdn-icons-png.flaticon.com/128/3670/3670151.png" width=5% height=5%></img></a>     <a href="https://www.reddit.com/user/yachay_ai"><img src="https://cdn-icons-png.flaticon.com/512/3670/3670226.png" width=5% height=5%></img></a>

