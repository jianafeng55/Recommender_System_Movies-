# MovieLens-Recommender

A pure Python implement of ``Collaborative Filtering``. Which contains ``User Based Collaborative Filtering``(UserCF) and ``Item Based Collaborative Filtering``(ItemCF). As comparisons, ``Random Based Recommendation`` and ``Most-Popular Based Recommendation`` are also included, too.

The buildin-datasets are ``Movielens-1M`` and ``Movielens-100k``. But you can of course use a custom dataset easily.

# Overview

The book 《[推荐系统实践](https://book.douban.com/subject/10769749/)》 written by *Xiang Liang* is quite wonderful for those people who don't have much knowledge about Recommendation System. But the book only offers each function of ``Collaborative Filtering``. Good structure, building datasets and model validation are required.

So I made ``MovieLens-Recommender`` project, which is a pure Python implement of ``Collaborative Filtering`` part based on the ideas of this book.

This repository is based on [MovieLens-RecSys][1], which is also a quit well implement of ``Collaborative Filtering``. But its efficiency is so damn poor!

Besides, [Surprise][2] is a very popular Python *scikit* building and analyzing recommender systems. So, I pick up the advantages of these two projects, and here comes ``MovieLens-Recommender``.

A common Recommendation System contains four steps:

- Create trainset and testset
- Train a recommender model
- Give recommendations
- Evaluate results

At the end of a recommendation process, four numbers are given to measure the recommendation model, which are:

- Precision
- Recall
- Coverage
- Popularity

**No python extensions(e.g. Numpy/pandas) are need!**

# Getting started

**1. Download**

``Git`` is awesome~

   ```shell
   git clone https://github.com/Lockvictor/MovieLens-RecSys.git
   ```

`Movielens-1M` and `Movielens-100k` are under the `data/` folder.

**2. Run**

The configures are in `main.py`. Pleas choose the dataset and model you want to use and set the proper test_size. The default values are shown below:

```python
dataset_name = 'ml-100k'
# dataset_name = 'ml-1m'
# model_type = 'UserCF'
# model_type = 'ItemCF'
model_type = 'Random'
# model_type = 'MostPopular'
test_size = 0.1
```

In your command line, run ``python main.py``. There will be a recommendation model built on the dataset you choose above.

Note: my code only test on python3, so python3 is prefer.

```shell
Python main.py
#Python3 main.py
```
if you are using Linux, this command will set the whole output into a file.

```shell
Python usercf.py > run.log 2>&1 &
#Python3 usercf.py > run.log 2>&1 &
```

This command will run in background. You can wait for the result, or use `tail -f run.log` to see the real time result.

All model will be saved to `model/` fold, which means the time will be cut down in your next run.

**3. Output**

Here is a example run result of ItemCF model trained on ml-1m with test_size = 0.10. No mater which model are chosen, the output log will like this.

```
**********************************************************************
    This is ItemCF model trained on ml-1m with test_size = 0.10
**********************************************************************

ItemBasedCF start...

No model saved before.
Train a new model...
counting movies number and popularity...
counting movies number and popularity success.
total movie number = 3693
generate items co-rated similarity matrix...
 steps(0), 0.00 seconds have spent..
 steps(1000), 18.50 seconds have spent..
 steps(2000), 46.39 seconds have spent..
 steps(3000), 63.52 seconds have spent..
 steps(4000), 87.37 seconds have spent..
 steps(5000), 111.83 seconds have spent..
 steps(6000), 132.71 seconds have spent..
generate items co-rated similarity matrix success.
total  step number is 6040
total 133.61 seconds have spent

calculate item-item similarity matrix...
 steps(0), 0.00 seconds have spent..
 steps(1000), 1.77 seconds have spent..
 steps(2000), 3.47 seconds have spent..
 steps(3000), 5.01 seconds have spent..
calculate item-item similarity matrix success.
total  step number is 3693
total 5.67 seconds have spent

Train a new model success.
The new model has saved success.

recommend for userid = 1:
['1196', '364', '1265', '318', '2081', '1282', '1198', '2716', '1', '2096']

recommend for userid = 100:
['2916', '1580', '457', '1240', '589', '1291', '780', '1036', '1610', '1214']

recommend for userid = 233:
['1022', '594', '1282', '2087', '2078', '1196', '608', '2081', '593', '1393']

recommend for userid = 666:
['296', '1704', '593', '356', '1196', '589', '1580', '50', '1393', '1']

recommend for userid = 888:
['2916', '457', '480', '2628', '1265', '1610', '1198', '1573', '2762', '1527']

Test recommendation system start...
 steps(0), 0.10 seconds have spent..
 steps(1000), 291.42 seconds have spent..
 steps(2000), 627.60 seconds have spent..
 steps(3000), 898.21 seconds have spent..
 steps(4000), 1219.94 seconds have spent..
 steps(5000), 1523.29 seconds have spent..
 steps(6000), 1817.46 seconds have spent..
Test recommendation system success.
total  step number is 6040
total 1829.26 seconds have spent

precision=0.1900	recall=0.1147	coverage=0.1673	popularity=7.3911

total Main Function step number is 0
total 1972.49 seconds have spent
```

# Benchmarks

Here are four models' benchmarks over Precision、Recall、Coverage、Popularity. The testsize is 0.1.

These results are nearly the same with the book, which prove that my algorithms are right.

**Movielens 1M:**

|    Movielens 1M    | Precision | Recall | Coverage | Popularity |
| :------------------: | --------: | -----: | -------: | ---------: |
| UserCF | 19.84% | 11.97% | 28.16% | 7.2023 |
| ItemCF | 19.00% | 11.47% | 16.73% | 7.3911 |
| Random | 0.54% | 0.33% | 100.00% | 4.4075 |
| Most Popular | 10.59% | 6.39% | 2.76% | 7.7462 |

**Movielens 100k:**

|    Movielens 100k    | Precision | Recall | Coverage | Popularity |
| :------------------: | --------: | -----: | -------: | ---------: |
| UserCF | 19.69% | 18.50% | 22.20% | 5.4928 |
| ItemCF | 17.89% | 16.80% | 13.23% | 5.6202 |
| Random | 0.82% | 0.77% | 99.64% | 3.0332 |
| Most Popular | 10.54% | 9.90% | 4.07% | 5.9578 |

# Attention

UserCF is faser than ItemCF. Using `ml-100k` instead of `ml-1m` will cut down the whole run time.

Caculate similarity matrix is quite slow. Please wait for the result patiently.


# Licence

Apache License.

    Copyright 2018 fuxuemingzhu

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


  [1]: https://github.com/Lockvictor/MovieLens-RecSys
  [2]: https://github.com/NicolasHug/Surprise
  [3]: http://www.apache.org/img/asf_logo.png