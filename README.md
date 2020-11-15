# Product-Recsys <a href="http://product-recsys.herokuapp.com/">applink</a>
[![Generic badge](https://img.shields.io/badge/Fastapi-<COLOR>.svg)](https://shields.io/) [![Generic badge](https://img.shields.io/badge/License-MIT-<COLOR>.svg)](https://shields.io/) 

In this project I utilized [Olist E-Commerce Public Dataset](https://www.kaggle.com/olistbr/brazilian-ecommerce), which has information of 100k orders from 2016 to 2018 made at multiple marketplaces in Brazil, to train 3 algorithms which generates product recommendations based on the ratings of products given by customers.

*Note: The granularity of transactions in the dataset is at product category level, thus recommendations are product categories in the true sense.*

The model training pipeline is [product-recsys-training](https://github.com/abhijitpai000/product-recsys-training) repository.

# Architecture
The website is divided into 3 sections.
1. **Top Trending** - Recommends highest rated products in the dataset.

      Methodology:
      
      [IMDB weighted average formula](https://help.imdb.com/article/imdb/track-movies-tv/ratings-faq/G67Y87TFYYP6TWAV#calculatetop) which takes into account the total number of reviews a product has recieved.

2. **Similar Products** - Takes user input of one product and recommends 5 similar products.

      Methodology:
      
      Computes cosine similarity between selected and other products using KNN Basic algorithm, as recommends 5 nearest neighbors.

3. **Products you might like** - Takes user input & rating of one product, and recommends 3 products based on the rating given for the selected product.

      Methodology:
      
      To make user specific recommendations it requires a sufficient amount of data to understand a user's taste. To solve this cold start problem, I approxiated user's taste by implementing two algorithms in the backend. The first, computes most similar user who has sufficient data and make recommendations based on their taste.

<img src="https://github.com/abhijitpai000/product_recommendation_system/blob/main/figures/backend_architecture.png?raw=true" alt="backend" width="918" height="429"/>

# Repository Structure
    .
    ├── backend
        └── models                                
            ├── similar_items_algo.pkl            # Trained algorithm from product-recsys-training repo.
            └── user_predictions_algo.pkl         # Trained algorithm from product-recsys-training repo.
        └── src
            ├── config.py                         # database configuration. 
            ├── trending.py                       # Returns top ten trending products.
            ├── item_rec_sys.py                   # Returns similar product recommendations using the ../models/similer_items_algo.pkl
            └── user_rec_sys.py                   # Returns similar product recommendations using the ../models/user_predictions_algo.pkl
    ├── frontend                                  # Front-end HTML and Javascript client side files for the website. 
    ├── main.py                                   # Fastapi API
    ├── requirements.txt                          
    ├── LICENSE
    └── README.md
