# CSCN8000 — Lab 2

## About this lab

In this lab, I worked on two different tasks using Python and Jupyter Notebook. First, I trained models to classify messages as spam or not spam. Then, I explored different ways to find and remove unusual prices from an Airbnb NYC dataset.

My goal was not only to run the code, but also to understand what each method does and how it changes the results.

## Part A — Spam Classification

I loaded the spam dataset and split it into 80% training data and 20% testing data. I used `CountVectorizer` to turn messages into word counts, then trained two models:

- Gaussian Naive Bayes
- Multinomial Naive Bayes

I compared the models using accuracy, precision, recall, F1-score, and confusion matrices. **MultinomialNB worked better on my test data**, reaching about **97.6% accuracy**, compared with **95.5% for GaussianNB**. I also used the trained model to make predictions on example messages.

## Part B — Airbnb NYC Data Cleaning

For this part, I focused on the price per night. I first removed missing and nonpositive prices. Then, I tried four outlier detection methods to see how they handled extreme values.

| Method | Rows kept | Data removed |
| --- | ---: | ---: |
| IQR | 45,912 | 6.08% |
| Percentile trimming (1%–99%) | 48,017 | 1.77% |
| Z-score (±3 standard deviations) | 48,496 | 0.79% |
| MAD (modified Z-score) | 45,968 | 5.97% |

I used summary statistics and boxplots to compare the results. I chose **IQR** for my final cleaned dataset because it uses quartiles and is less affected by extreme prices than methods based on the mean.

After that, I checked that the prices were not missing, were greater than zero, and were within the IQR limits. I saved the final dataset as **`airbnb_nyc_cleaned.csv`**, with **45,912 rows**.

I also tried **Groupwise IQR** to compare prices within each Airbnb room type. It kept **45,640 rows**. This was a separate experiment, not the dataset I exported as my final result.

## My observation

I noticed that each method handled outliers differently. IQR and MAD removed more extreme prices, while Z-score kept more data. I also realized that prices depend on the room type. A high price for a shared room might be normal for an entire apartment. This helped me understand that data cleaning is not just about removing values. I need to understand the data before deciding what to keep.

## How to run the notebook

Keep the notebook and datasets in this folder structure:

```text
Lab2/
├── Lab2.ipynb
├── README.md
└── data/
    ├── lab2_spam.csv
    └── AB_NYC_2019.csv
```

You will need Python, Jupyter Notebook, and the following libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`.

Open `Lab2.ipynb` and run the cells from top to bottom. The notebook saves the cleaned Airbnb dataset as a CSV file.

To export the notebook as HTML for submission, use:

```bash
jupyter nbconvert --to html Lab2.ipynb
```

The assignment asks for both the **`.ipynb` notebook** and the **`.html` file**.

## AI acknowledgment

I used **ChatGPT by OpenAI** as a learning assistant while working on this lab. It helped me understand the Python code and statistical methods, compare the outlier detection results, and improve my English explanations and this README. I used these explanations to support my learning and reviewed the work in my notebook.
