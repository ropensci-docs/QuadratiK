# Wireless Indoor Localization

The `wireless` data frame has 2000 rows and 8 columns. The first 7
variables report the measurements of the Wi-Fi signal strength received
from 7 Wi-Fi routers in an office location in Pittsburgh (USA). The last
column indicates the class labels.

## Usage

``` r
wireless
```

## Format

A data frame containing the following columns:

- `V1` Signal strength from router 1.

- `V2` Signal strength from router 2.

- `V3` Signal strength from router 3.

- `V4` Signal strength from router 4.

- `V5` Signal strength from router 5.

- `V6` Signal strength from router 6.

- `V7` Signal strength from router 7.

- `V8` Group memberships, from 1 to 4.

## Source

Bhatt, R. (2017). Wireless Indoor Localization. UCI Machine Learning
Repository.  
https://doi.org/10.24432/C51880.

## Details

The Wi-Fi signal strength is measured in dBm, decibel milliwatts, which
is expressed as a negative value ranging from -100 to 0. The labels
correspond to 4 different rooms. In total, we have 4 groups with 500
observations each.

## References

Rohra, J.G., Perumal, B., Narayanan, S.J., Thakur, P. and Bhatt, R.B.
(2017). "User Localization in an Indoor Environment Using Fuzzy Hybrid
of Particle Swarm Optimization & Gravitational Search Algorithm with
Neural Networks". In: Deep, K., et al. Proceedings of Sixth
International Conference on Soft Computing for Problem Solving. Advances
in Intelligent Systems and Computing, vol 546. Springer, Singapore.
https://doi.org/10.1007/978-981-10-3322-3_27

## Examples

``` r
data(wireless)
summary(wireless)
#>        V1               V2               V3               V4        
#>  Min.   :-74.00   Min.   :-74.00   Min.   :-73.00   Min.   :-77.00  
#>  1st Qu.:-61.00   1st Qu.:-58.00   1st Qu.:-58.00   1st Qu.:-63.00  
#>  Median :-55.00   Median :-56.00   Median :-55.00   Median :-56.00  
#>  Mean   :-52.33   Mean   :-55.62   Mean   :-54.96   Mean   :-53.57  
#>  3rd Qu.:-46.00   3rd Qu.:-53.00   3rd Qu.:-51.00   3rd Qu.:-46.00  
#>  Max.   :-10.00   Max.   :-45.00   Max.   :-40.00   Max.   :-11.00  
#>        V5               V6               V7               V8      
#>  Min.   :-89.00   Min.   :-97.00   Min.   :-98.00   Min.   :1.00  
#>  1st Qu.:-69.00   1st Qu.:-86.00   1st Qu.:-87.00   1st Qu.:1.75  
#>  Median :-64.00   Median :-82.00   Median :-83.00   Median :2.50  
#>  Mean   :-62.64   Mean   :-80.98   Mean   :-81.73   Mean   :2.50  
#>  3rd Qu.:-56.00   3rd Qu.:-77.00   3rd Qu.:-78.00   3rd Qu.:3.25  
#>  Max.   :-36.00   Max.   :-61.00   Max.   :-63.00   Max.   :4.00  
```
