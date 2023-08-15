# Perfume Recommender System
<p align="center">
<img src="images\perfume_cover.jpg" class="center" width="35%"/>
</p>

## Overview
A recommendation system, also known as a recommender system, is a class of algorithms and techniques used in information filtering and decision-making processes. Its main purpose is to provide personalized suggestions or recommendations to users for items they might be interested in. These items could be products, services, movies, music, articles, or anything else that can be recommended based on user preferences and behavior. In this work, a perfume recommendation system will be built based on the scent description.

## Objectives
Create a perfume recommendation app based on its scents. 

## Tecnologies Used
* python 3.9.16
* pandas 1.5.3
* numpy 1.22.4
* sklearn 1.2.2
* scipy 1.10.0
* gradio 3.39.0

## About the Data
The data was scrapped from site fragrantica.com [1]. The dataset contains 2.570 unique brands, 36.969 perfumes and 2.145 different scents.

## Methodology
Fragrance notes are the individual scent layers of ingredients that make up a fragrance. They are the building blocks of a fragrance and contribute to its overall scent profile. Fragrance notes are typically categorized into three main types: top notes, heart notes (also known as middle or mid notes), and base notes. Each note plays a specific role in the fragrance’s development and longevity [2]. 
<p align="center">
<img src="images\notes.png" class="center" width="80%"/>
</p>

For this work, we grouped the scents in a single description, given that not all samples in the dataset have the scent division by notes, even though such division influences the performance and, consequently, the real similarity between perfumes.

The first task of text clean up was relatively simple, as the fields on the site were standardized. We just had to remove some special characters, leave the text in lower case and group the note subcategories (top, middle and base) into a single category. After this step, the perfume scents were vectorized using bag of words method from sklearn. We chose this method for it's simplicity and good results for this specific case.

The cosine method was used for similarity calculation. Due to memory limitations for storing the resultant matrix (36969 x 36969), we used sparse output method. Our application gonna use a pre-calculated base of similarities, for this reason, we saved two matrices: One for perfume index `vect_index` and another for similarities values `vect_values` resulting from the cosine calculation. We saved both on pickle format.

Finally, we used gradio to build a demo app, capable of performing the recommendation task based on brand and perfume name choices.

## Results and Conclusions
Even with limited resources and some assumptions adopted, it was possible to create a pretty decent recommend system, capable of delivering acceptable results. Below, a print of the developed App.

<p align="center">
<img src="images\app_gradio.png" class="center" width="100%"/>
</p>

This work came from a personal need, where a perfume that I really like (Hugo Boss Soul) stopped being marketed. Unfortunately I couldn't find the first place in the list generated (Shirley May - Compass), but the second place can be easily found (Carolina Herrera - 212 Men White). I'll probably give it a chance...


**Future improvements proposal:** As mentioned above, the division of scents into notes is crucial for the characteristic of perfumes. Unfortunately, the dataset used didn't have this division for all elements. Certainly, a richer dataset could yield better results. Thinking about text embedding, for this solution, the simplest form of vectorization (bag of words) was employed, but other methodologies could also be tested, such as TF-IDF, Word2vec, FastText, Doc2vec, and even transformers.

## References
* [1] https://www.fragrantica.com/
* [2] https://www.fragrancex.com/blog/fragrance-notes/
