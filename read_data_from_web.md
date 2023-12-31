Read Data From the Web
================

Load the necessary libraries.

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
```

Import NSDUH data

``` r
nsduh_url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

nsduh_html = 
  read_html(nsduh_url)
```

``` r
marj_use_df=
nsduh_html|>
  html_table()|>
  first() |>
  #we have 15 lists and we just take the first table
  slice(-1)#remove the first line of notes
```

Import star wars …

``` r
swm_html = 
  read_html("https://www.imdb.com/list/ls070150896/")
```

``` r
smv_title_vec=
  swm_html|>
  html_elements(".lister-item-header a")|>
  html_text()
```

``` r
smv_gross_rev_vec=
  swm_html|>
  html_elements(".text-muted .ghost~ .text-muted+ span")|>
  html_text()
```

``` r
swm_df=
  tibble(
    title=smv_title_vec,
    gross_rev=smv_gross_rev_vec
  )
```
