# Restaurant-Search-Copilot
## Getting Started
Colab link:
https://colab.research.google.com/drive/1l0qnwW2H5YQHWcQnVtYw-Pr5YErXZU7I?usp=sharing

Or access the `main.ipynb` under the repo. 

## Data Loading
If you want to get the direct open sources of Yelp Dataset, please access the link: https://www.yelp.com/dataset. 

Following the use agreement of the Yelp dataset: https://s3-media0.fl.yelpcdn.com/assets/srv0/engineering_pages/f64cb2d3efcc/assets/vendor/Dataset_User_Agreement.pdf

In my Colab notebook, I preprocessed the dataset and stored the data frames for convenience. Due to the user agreement, I cannot provide the my preprocessed dataset files.

The original files of Yelp dataset are JSON files. In Python, you can read the JSON files like this (using the json and pandas libraries):
```Ruby

import json
import pandas as pd
data_file = open("yelp_academic_dataset_review.json")
data = []
for line in data_file:
&nbsp;data.append(json.loads(line))
checkin_df = pd.DataFrame(data)
data_file.close()

```

## Model Loading
I have already pre-trained the LSTM model for the classification. I provided the pre-trained model file in this link: https://drive.google.com/file/d/1YkxaaeMQEGkZjxQ19dsoEWxSAIK8EMUi/view?usp=drive_link

To load the pre-trained model, please check the `Model Loading` section in my notebook. And using the below codes:
Before running the code, please make sure you finish the uploading of the pre-trained model file in the notebook.

```Ruby

import pickle
saved_lstm = pickle.load(open('lstm', 'rb'))

```

## Result demonstration
After you finished all the data and model loading, please run the `Review Cleaning and Extraction` and `Word tokenization` sections.

**Notice: make sure your data frame's name is the same as the `review_df` and `business_df` to avoid the possible errors**

Then go to the `Recommendation` section, run the code chuck:

```Ruby

review = "The pretzel is good.A nice French restaurant in the Park Slope."
returned = predict_review(review)
for i, item in enumerate(returned[0]):
    if item == 1:
        prediction = i
        break
print(f'{review[:100]} -> {prediction:.2f}')

```
You can change the `review` on the first line to make the change on the user's review input.

In this chuck below, you can match the business name of reviews and get a recommendation:

```Ruby
name = "La Creperie"
recommendations = get_recommendations(name,cosine_sim)
print(f"Recommendations for {name} from high to low:")
print(recommendations)
```
Run this chuck below, you can get the geographical visualization of recommendation.

```Ruby
import folium

m = folium.Map(location=[recommendations['latitude'].mean(), recommendations['longitude'].mean()], zoom_start=5)

# Add a marker for each location in the DataFrame
for index, row in recommendations.iterrows():
    folium.Marker([row['latitude'], row['longitude']], popup=row['name']).add_to(m)

# Display the map
m
```

## More Information and details

For more theoretical explanation, please check the written documentation `Appendix.pdf` in this Github repo.
