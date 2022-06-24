Spotify Music
================
Mizukiki
6/23/2022

## Import Data

``` r
data_path = "https://storage.googleapis.com/kagglesdsdata/datasets/1833/3172/data.csv?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=gcp-kaggle-com%40kaggle-161607.iam.gserviceaccount.com%2F20220624%2Fauto%2Fstorage%2Fgoog4_request&X-Goog-Date=20220624T021748Z&X-Goog-Expires=259199&X-Goog-SignedHeaders=host&X-Goog-Signature=53d8f4f758edbad10ec165dd5b5290cbcaaa7715d77d5abdab6a708d36c6e381151f1e937aaf2dd989c45b3c150698fe13fd5908dc42b41cc02a9b806330fa760f4c62e43b317b349663fd8c8ed8820ff721982d6aed16a812c4ca44541cc81ba3dd92089d76cdd1dbf868b1c23ed4664a3e1d895cb605abc7a4637ee45358e974fed78d7b65f978a88544c721d8d94a2a90777cf3354d8f8ad585bad6fe113b58bd4007d6d2017c348f0cc27df56eb1222fad62a2c256186b96c91950a52a187c4d97e9c50ee31a5f786eb3ddf4124bacafaa86d0420288e976bcb41f8be81275f90ac100de540bff726f789ab57b19789c9fa051905f54df3b3fd6e3f0acdc"

data = read.csv(data_path)

str(data)
```

    ## 'data.frame':    2017 obs. of  17 variables:
    ##  $ X               : int  0 1 2 3 4 5 6 7 8 9 ...
    ##  $ acousticness    : num  0.0102 0.199 0.0344 0.604 0.18 0.00479 0.0145 0.0202 0.0481 0.00208 ...
    ##  $ danceability    : num  0.833 0.743 0.838 0.494 0.678 0.804 0.739 0.266 0.603 0.836 ...
    ##  $ duration_ms     : int  204600 326933 185707 199413 392893 251333 241400 349667 202853 226840 ...
    ##  $ energy          : num  0.434 0.359 0.412 0.338 0.561 0.56 0.472 0.348 0.944 0.603 ...
    ##  $ instrumentalness: num  2.19e-02 6.11e-03 2.34e-04 5.10e-01 5.12e-01 0.00 7.27e-06 6.64e-01 0.00 0.00 ...
    ##  $ key             : int  2 1 2 5 5 8 1 10 11 7 ...
    ##  $ liveness        : num  0.165 0.137 0.159 0.0922 0.439 0.164 0.207 0.16 0.342 0.571 ...
    ##  $ loudness        : num  -8.79 -10.4 -7.15 -15.24 -11.65 ...
    ##  $ mode            : int  1 1 1 1 0 1 1 0 0 1 ...
    ##  $ speechiness     : num  0.431 0.0794 0.289 0.0261 0.0694 0.185 0.156 0.0371 0.347 0.237 ...
    ##  $ tempo           : num  150.1 160.1 75 86.5 174 ...
    ##  $ time_signature  : num  4 4 4 4 4 4 4 4 4 4 ...
    ##  $ valence         : num  0.286 0.588 0.173 0.23 0.904 0.264 0.308 0.393 0.398 0.386 ...
    ##  $ target          : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ song_title      : chr  "Mask Off" "Redbone" "Xanny Family" "Master Of None" ...
    ##  $ artist          : chr  "Future" "Childish Gambino" "Future" "Beach House" ...

``` r
summary(data)
```

    ##        X         acousticness        danceability     duration_ms     
    ##  Min.   :   0   Min.   :0.0000028   Min.   :0.1220   Min.   :  16042  
    ##  1st Qu.: 504   1st Qu.:0.0096300   1st Qu.:0.5140   1st Qu.: 200015  
    ##  Median :1008   Median :0.0633000   Median :0.6310   Median : 229261  
    ##  Mean   :1008   Mean   :0.1875900   Mean   :0.6184   Mean   : 246306  
    ##  3rd Qu.:1512   3rd Qu.:0.2650000   3rd Qu.:0.7380   3rd Qu.: 270333  
    ##  Max.   :2016   Max.   :0.9950000   Max.   :0.9840   Max.   :1004627  
    ##      energy       instrumentalness         key            liveness     
    ##  Min.   :0.0148   Min.   :0.0000000   Min.   : 0.000   Min.   :0.0188  
    ##  1st Qu.:0.5630   1st Qu.:0.0000000   1st Qu.: 2.000   1st Qu.:0.0923  
    ##  Median :0.7150   Median :0.0000762   Median : 6.000   Median :0.1270  
    ##  Mean   :0.6816   Mean   :0.1332855   Mean   : 5.343   Mean   :0.1908  
    ##  3rd Qu.:0.8460   3rd Qu.:0.0540000   3rd Qu.: 9.000   3rd Qu.:0.2470  
    ##  Max.   :0.9980   Max.   :0.9760000   Max.   :11.000   Max.   :0.9690  
    ##     loudness            mode         speechiness          tempo       
    ##  Min.   :-33.097   Min.   :0.0000   Min.   :0.02310   Min.   : 47.86  
    ##  1st Qu.: -8.394   1st Qu.:0.0000   1st Qu.:0.03750   1st Qu.:100.19  
    ##  Median : -6.248   Median :1.0000   Median :0.05490   Median :121.43  
    ##  Mean   : -7.086   Mean   :0.6123   Mean   :0.09266   Mean   :121.60  
    ##  3rd Qu.: -4.746   3rd Qu.:1.0000   3rd Qu.:0.10800   3rd Qu.:137.85  
    ##  Max.   : -0.307   Max.   :1.0000   Max.   :0.81600   Max.   :219.33  
    ##  time_signature     valence           target        song_title       
    ##  Min.   :1.000   Min.   :0.0348   Min.   :0.0000   Length:2017       
    ##  1st Qu.:4.000   1st Qu.:0.2950   1st Qu.:0.0000   Class :character  
    ##  Median :4.000   Median :0.4920   Median :1.0000   Mode  :character  
    ##  Mean   :3.968   Mean   :0.4968   Mean   :0.5057                     
    ##  3rd Qu.:4.000   3rd Qu.:0.6910   3rd Qu.:1.0000                     
    ##  Max.   :5.000   Max.   :0.9920   Max.   :1.0000                     
    ##     artist         
    ##  Length:2017       
    ##  Class :character  
    ##  Mode  :character  
    ##                    
    ##                    
    ## 

## Data Exploratory

Filter out artist with only one song:

``` r
song_cnt = data %>% group_by(artist) %>% 
    count(artist) %>% 
    filter(n > 1)
```

Artist’s key distribution

``` r
key_dist = data[match(data$artist, song_cnt$artist),] %>% 
    group_by(artist) %>% 
    summarize(key_median = median(key), 
              avg_key = mean(key), 
              hightest_key = max(key), 
              lowest_key = min(key), 
              diff = max(key) - min(key)) 

str(key_dist)
```

    ## tibble [266 × 6] (S3: tbl_df/tbl/data.frame)
    ##  $ artist      : chr [1:266] "20th Century Steel Band" "2milly" "A-Trak" "A$AP Rocky" ...
    ##  $ key_median  : num [1:266] 2 2 11 2 8 5 0 9 6 1 ...
    ##  $ avg_key     : num [1:266] 2 2 11 2 8 5 0 9 6 1 ...
    ##  $ hightest_key: int [1:266] 2 2 11 2 8 5 0 9 6 1 ...
    ##  $ lowest_key  : int [1:266] 2 2 11 2 8 5 0 9 6 1 ...
    ##  $ diff        : int [1:266] 0 0 0 0 0 0 0 0 0 0 ...

Can Answer following questions: Which artist has the widest range? Which
artist has the narrowest range? Which artist has the highest tone on
average?

``` r
key_dist[which.max(key_dist$diff),] %>% knitr::kable()
```

| artist     | key\_median | avg\_key | hightest\_key | lowest\_key | diff |
| :--------- | ----------: | -------: | ------------: | ----------: | ---: |
| Disclosure |          10 |      8.1 |            11 |           0 |   11 |

``` r
key_dist[which.min(key_dist$diff),] %>% knitr::kable()
```

| artist                  | key\_median | avg\_key | hightest\_key | lowest\_key | diff |
| :---------------------- | ----------: | -------: | ------------: | ----------: | ---: |
| 20th Century Steel Band |           2 |        2 |             2 |           2 |    0 |

``` r
key_dist[which.max(key_dist$avg_key),] %>% knitr::kable()
```

| artist | key\_median | avg\_key | hightest\_key | lowest\_key | diff |
| :----- | ----------: | -------: | ------------: | ----------: | ---: |
| A-Trak |          11 |       11 |            11 |          11 |    0 |

Pull out the song title with widest/narrowest from the dataset.

``` r
data %>% filter(artist == "Disclosure" | artist == "20th Century Steel Band") %>% select(artist, song_title, key) %>%  filter(key == 11 | key == 2) %>% knitr::kable()
```

| artist                  | song\_title                 | key |
| :---------------------- | :-------------------------- | --: |
| Disclosure              | Bang That                   |  11 |
| 20th Century Steel Band | Heaven And Hell Is On Earth |   2 |

Are these artist only have one song?
