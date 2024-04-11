# Restaurant-Search-Copilot
## Getting started
Colab link:
https://colab.research.google.com/drive/1l0qnwW2H5YQHWcQnVtYw-Pr5YErXZU7I?usp=sharing

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


