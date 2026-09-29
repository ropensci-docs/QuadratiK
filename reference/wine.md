# Wine data set

The `wine` data frame has 178 rows and 14 columns. The first 13
variables report 13 constituents found in each of the three types of
wines. The last column indicates the class labels (1,2 or 3).

## Usage

``` r
wine
```

## Format

A data frame containing the following columns:

- `Alcohol`

- `Malic acid`

- `Ash`

- `Alcalinity of ash`

- `Magnesium`

- `Total phenols`

- `Flavanoids`

- `Nonflavanoid phenols`

- `Proanthocyanins`

- `Color intensity`

- `Hue`

- `OD280/OD315 of diluted wines`

- `Proline`

- `y`: class membership

## Source

Aeberhard, S. and Forina, M. (1991). Wine. UCI Machine Learning
Repository. https://doi.org/10.24432/C5PC7J.

## Details

These data are the results of a chemical analysis of wines grown in the
same region in Italy but derived from three different cultivars. The
analysis determined the quantities of 13 constituents found in each of
the three types of wines.

## References

Aeberhard, S., Coomans, D. and De Vel, O. (1994). Comparative analysis
of statistical pattern recognition methods in high dimensional settings.
Pattern Recognition, 27(8), 1065-1077.

## Examples

``` r
data(wine)
summary(wine)
#>     Alcohol        Malicacid          Ash        Alcalinity_of_ash
#>  Min.   :11.03   Min.   :0.740   Min.   :1.360   Min.   :10.60    
#>  1st Qu.:12.36   1st Qu.:1.603   1st Qu.:2.210   1st Qu.:17.20    
#>  Median :13.05   Median :1.865   Median :2.360   Median :19.50    
#>  Mean   :13.00   Mean   :2.336   Mean   :2.367   Mean   :19.49    
#>  3rd Qu.:13.68   3rd Qu.:3.083   3rd Qu.:2.558   3rd Qu.:21.50    
#>  Max.   :14.83   Max.   :5.800   Max.   :3.230   Max.   :30.00    
#>    Magnesium      Total_phenols     Flavanoids    Nonflavanoid_phenols
#>  Min.   : 70.00   Min.   :0.980   Min.   :0.340   Min.   :0.1300      
#>  1st Qu.: 88.00   1st Qu.:1.742   1st Qu.:1.205   1st Qu.:0.2700      
#>  Median : 98.00   Median :2.355   Median :2.135   Median :0.3400      
#>  Mean   : 99.74   Mean   :2.295   Mean   :2.029   Mean   :0.3619      
#>  3rd Qu.:107.00   3rd Qu.:2.800   3rd Qu.:2.875   3rd Qu.:0.4375      
#>  Max.   :162.00   Max.   :3.880   Max.   :5.080   Max.   :0.6600      
#>  Proanthocyanins Color_intensity       Hue        
#>  Min.   :0.410   Min.   : 1.280   Min.   :0.4800  
#>  1st Qu.:1.250   1st Qu.: 3.220   1st Qu.:0.7825  
#>  Median :1.555   Median : 4.690   Median :0.9650  
#>  Mean   :1.591   Mean   : 5.058   Mean   :0.9574  
#>  3rd Qu.:1.950   3rd Qu.: 6.200   3rd Qu.:1.1200  
#>  Max.   :3.580   Max.   :13.000   Max.   :1.7100  
#>  X0D280_0D315_of_diluted_wines    Proline             y        
#>  Min.   :1.270                 Min.   : 278.0   Min.   :1.000  
#>  1st Qu.:1.938                 1st Qu.: 500.5   1st Qu.:1.000  
#>  Median :2.780                 Median : 673.5   Median :2.000  
#>  Mean   :2.612                 Mean   : 746.9   Mean   :1.938  
#>  3rd Qu.:3.170                 3rd Qu.: 985.0   3rd Qu.:3.000  
#>  Max.   :4.000                 Max.   :1680.0   Max.   :3.000  
```
