\#output: html\_document

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.4     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readr)
```

<a href="https://github.com/fredhutchio/tfcb_capstone" class="uri">https://github.com/fredhutchio/tfcb_capstone</a>
<a href="https://www.markdownguide.org/cheat-sheet" class="uri">https://www.markdownguide.org/cheat-sheet</a>
\#\#About the Data This is where I talk about the data, assumptions etc

The dataset that I chose to investigate further was the
[Immunohistochemical typing of
adenocarcinomas](https://datadryad.org/stash/dataset/doi:10.5061/dryad.g8h71).
I am specifically working with the dataset that is found in the
[“pcbil\_clinicaldata.xlsx”](data/pcbil_clinicaldata.xlsx) in the “PLOS
Revision” tab. I have placed the data that was in the “PLOS Revision”
tab into a new csv file found
[here](data/pcbil_clinicaldata_PLOS_REVISION.csv)

Project organization
--------------------

Information about things in this project

Within the data folder, I have placed the dataset that I extracted from
DRYAD. The dataset had a “pcbil\_clinicaldata.xlsx” excelsheet but in
order to make dtaaframes in Python, I made separate CSV files for each
sheet in the excel workbook.

Data
----

Citation and link to data

About the analysis
------------------

Information about other things useful to know for the context of the
overall project.

\#\#Reproducibility

Problem 1
---------

**10 points**

For each of the following functions, provide a &lt;100 character
description (in your own words) and a URL reference.

1.  `!` This mean “not”. For example, when using the logical operator
    “!=” this would mean “not equal to”
    [.](https://www.statmethods.net/management/operators.html)

2.  `is.na` This is a function that can be used to search for missing
    values in a dataset, returning true if NA
    [present.](https://www.programmingr.com/tutorial/is-na/#:~:text=Find%20missing%20values%20in%20R,to%20a%20value%20of%20false.)

3.  `is.numeric` This function test returns ‘True’ if all numbers in the
    dataset or object tested are
    [numeric.](https://www.rdocumentation.org/packages/base/versions/3.3/topics/numeric)

4.  `anti_join` This takes two arguments (let’s say x/y) and returns all
    rows from x where it does not match values in
    [y.](http://zevross.com/blog/2014/08/05/using-the-r-function-anti_join-to-find-unmatched-records/)

5.  `desc` This is a function that takes the vector as the input and
    transforms it so that the data can be sorted in descending
    [order.](https://www.rdocumentation.org/packages/plyr/versions/1.8.6/topics/desc)

6.  `slice` This is a function that will only depict rows of interest
    from some dataset. For instance: data %&gt;% slice (1:10)
    [.](https://dplyr.tidyverse.org/articles/base.html?q=slice#slice-choose-rows-by-position)

7.  `all_vars` This is a function that is used often with filter()
    functions to return variables that are True and meet the condition
    [ex)
    all\_vars(. &gt;= 100)](https://dplyr.tidyverse.org/reference/all_vars.html)

8.  `funs` Funs is a function that creates a lit of functions. So you
    can create a list that contains only the mean, max, and median
    functions
    [.](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/funs)

9.  `filter_if` This is a filtering function that will filter for
    variables/rows/etc that meet a specific
    [condition.](http://thatdatatho.com/2019/04/08/more-dplyr-get-data-into-right-shape/)

10. `mutate_if` This function is used to transform/affect multiple
    variables that meet a specific
    [condition.](http://thatdatatho.com/2019/04/08/more-dplyr-get-data-into-right-shape/)

Problem 2
---------

**10 points**

Add a comment above each code line below explaining what the code line
does and/or why that code line is necessary.

Keep each comment to less than 2 lines per line of code and &lt; 80
chars per line.

``` r
# You are reading in the tsv file into a tibble assigned as 'annotations'.
annotations <- read_tsv("ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt") %>%
  #Using pipe %>% operator to chain commands. Select() command will only keep variables mentioned.
  select(ensembl_gene_id, symbol, name, gene_family, ccds_id) %>%
  #Further pipe `annotations` to filter for all data except instances where the ccds_id is not known.
  filter(!is.na(ccds_id)) %>%
  #Now you are printing what you have selected and filtered with the chained commands. 
  print()
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   .default = col_character(),
    ##   date_approved_reserved = col_date(format = ""),
    ##   date_symbol_changed = col_date(format = ""),
    ##   date_name_changed = col_date(format = ""),
    ##   date_modified = col_date(format = ""),
    ##   entrez_id = col_double(),
    ##   mirbase = col_logical(),
    ##   homeodb = col_double(),
    ##   snornabase = col_logical(),
    ##   bioparadigms_slc = col_logical(),
    ##   orphanet = col_double(),
    ##   horde_id = col_logical(),
    ##   imgt = col_logical(),
    ##   kznf_gene_catalog = col_logical(),
    ##   `mamit-trnadb` = col_logical(),
    ##   lncrnadb = col_logical(),
    ##   intermediate_filament_db = col_logical(),
    ##   rna_central_ids = col_logical(),
    ##   gtrnadb = col_logical()
    ## )
    ## ℹ Use `spec()` for the full column specifications.

    ## Warning: 1410 parsing failures.
    ##  row                      col           expected    actual                                                                                       file
    ## 1475 kznf_gene_catalog        1/0/T/F/TRUE/FALSE 404       'ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt'
    ## 1483 kznf_gene_catalog        1/0/T/F/TRUE/FALSE 341       'ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt'
    ## 1484 kznf_gene_catalog        1/0/T/F/TRUE/FALSE 90        'ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt'
    ## 1521 intermediate_filament_db 1/0/T/F/TRUE/FALSE HGNC:1040 'ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt'
    ## 1522 intermediate_filament_db 1/0/T/F/TRUE/FALSE HGNC:1041 'ftp://ftp.ebi.ac.uk/pub/databases/genenames/new/tsv/locus_groups/protein-coding_gene.txt'
    ## .... ........................ .................. ......... ..........................................................................................
    ## See problems(...) for more details.

    ## # A tibble: 18,835 x 5
    ##    ensembl_gene_id symbol  name            gene_family            ccds_id       
    ##    <chr>           <chr>   <chr>           <chr>                  <chr>         
    ##  1 ENSG00000121410 A1BG    alpha-1-B glyc… Immunoglobulin like d… CCDS12976     
    ##  2 ENSG00000148584 A1CF    APOBEC1 comple… RNA binding motif con… CCDS73133|CCD…
    ##  3 ENSG00000175899 A2M     alpha-2-macrog… C3 and PZP like, alph… CCDS44827     
    ##  4 ENSG00000166535 A2ML1   alpha-2-macrog… C3 and PZP like, alph… CCDS73439|CCD…
    ##  5 ENSG00000184389 A3GALT2 alpha 1,3-gala… Glycosyltransferase f… CCDS60080     
    ##  6 ENSG00000128274 A4GALT  alpha 1,4-gala… Alpha 1,4-glycosyltra… CCDS14041     
    ##  7 ENSG00000118017 A4GNT   alpha-1,4-N-ac… Alpha 1,4-glycosyltra… CCDS3097      
    ##  8 ENSG00000094914 AAAS    aladin WD repe… WD repeat domain cont… CCDS8856|CCDS…
    ##  9 ENSG00000081760 AACS    acetoacetyl-Co… Acyl-CoA synthetase f… CCDS9263      
    ## 10 ENSG00000114771 AADAC   arylacetamide … Lipases|Arylacetamide… CCDS33877     
    ## # … with 18,825 more rows

``` r
# You are reading in the tsv file into a tibble assigned as 'data'.Pipe operator to chain commands
data <- read_tsv("ftp://ftp.ncbi.nlm.nih.gov/geo/series/GSE89nnn/GSE89183/suppl/GSE89183_Counts.txt.gz") %>%
  #Chained command is rename() to change column name. 
  rename(ensembl_gene_id = "ENSEMBL gene") %>%
  #Now printing all rows of 'data' dataset
  print()
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   `ENSEMBL gene` = col_character(),
    ##   CD34_shTSR2_RNA_1 = col_double(),
    ##   CD34_shTSR2_RNA_2 = col_double(),
    ##   CD34_shRPL5_RNA_1 = col_double(),
    ##   CD34_shRPL5_RNA_2 = col_double(),
    ##   CD34_shRPL5_RPF_1 = col_double(),
    ##   CD34_shRPL5_RPF_2 = col_double(),
    ##   CD34_shRPS19_RNA_1 = col_double(),
    ##   CD34_shRPS19_RNA_2 = col_double(),
    ##   CD34_shRPS19_RPF_1 = col_double(),
    ##   CD34_shRPS19_RPF_2 = col_double(),
    ##   CD34_shLuc_RNA_1 = col_double(),
    ##   CD34_shLuc_RNA_2 = col_double(),
    ##   CD34_shLuc_RPF_1 = col_double(),
    ##   CD34_shLuc_RPF_2 = col_double()
    ## )

    ## # A tibble: 63,677 x 15
    ##    ensembl_gene_id CD34_shTSR2_RNA… CD34_shTSR2_RNA… CD34_shRPL5_RNA…
    ##    <chr>                      <dbl>            <dbl>            <dbl>
    ##  1 ENSG00000000003               48               56               40
    ##  2 ENSG00000000005                0                2                0
    ##  3 ENSG00000000419              880              744             1116
    ##  4 ENSG00000000457              124              113              149
    ##  5 ENSG00000000460              249              262              289
    ##  6 ENSG00000000938               89               64              204
    ##  7 ENSG00000000971              106               86              241
    ##  8 ENSG00000001036              897              613             1487
    ##  9 ENSG00000001084              965             1027             1036
    ## 10 ENSG00000001167              721              835              498
    ## # … with 63,667 more rows, and 11 more variables: CD34_shRPL5_RNA_2 <dbl>,
    ## #   CD34_shRPL5_RPF_1 <dbl>, CD34_shRPL5_RPF_2 <dbl>, CD34_shRPS19_RNA_1 <dbl>,
    ## #   CD34_shRPS19_RNA_2 <dbl>, CD34_shRPS19_RPF_1 <dbl>,
    ## #   CD34_shRPS19_RPF_2 <dbl>, CD34_shLuc_RNA_1 <dbl>, CD34_shLuc_RNA_2 <dbl>,
    ## #   CD34_shLuc_RPF_1 <dbl>, CD34_shLuc_RPF_2 <dbl>

``` r
#write_csv(data, "hw_6_file.tsv") 
```

Problem 3
---------

**10 points**

Using the code below:

\#1. Convert both axes to `log10` instead of linear scales. \#2. Show
axis tick labels as 10<sup>0</sup>, 10<sup>1</sup>,
10<sup>2</sup>,10<sup>3</sup>, 10<sup>4</sup>, 10<sup>5</sup> for both
axes. \#3. There are too many points overlapping in certain regions. Use
a different `geom_` function to convey to your reader how many
overlapping points are present in each region.

``` r
data %>%
  select(CD34_shRPL5_RNA_1, CD34_shRPS19_RNA_1) %>%
  ggplot(aes(x = CD34_shRPL5_RNA_1, y = CD34_shRPS19_RNA_1)) +
  #geom_hex(binwidth = c(.1, 500), stat = "binhex",) +
  geom_bin2d(binwidth = c(0.1, 0.1)) +
  scale_x_log10(
    breaks= c(1, 10, 100, 1000, 10000, 100000), 
    labels= c("10^0", "10^1", "10^2", "10^3", "10^4", "10^5")) +
  scale_y_log10(
    breaks= c(1, 10, 100, 1000, 10000, 100000), 
    labels= c("10^0", "10^1", "10^2", "10^3", "10^4", "10^5")) #+
```

    ## Warning: Transformation introduced infinite values in continuous x-axis

    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## Warning: Removed 43031 rows containing non-finite values (stat_bin2d).

![](README2_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
  #labs(x = "Kozak region", y= "Mean ratio", title= "Effect of Kozak region on protein expression")

#"10^0", "10^1", "10^2", "10^3", "10^4", "10^5"
#geom_count()
```

**In problems 4 through 6, assign the result of your operation back to
the `data` variable.**

Problem 4
---------

**10 points**

Write a code chunk to select the following columns from the `data`
variable you created above and reassign back to `data`.

``` r
data <-data %>%
  select(ensembl_gene_id, CD34_shRPL5_RPF_1, CD34_shRPL5_RPF_2, CD34_shRPL5_RNA_1, CD34_shRPL5_RNA_2,
         CD34_shRPS19_RPF_1, CD34_shRPS19_RPF_2, CD34_shRPS19_RNA_1, CD34_shRPS19_RNA_2, CD34_shLuc_RPF_1,
         CD34_shLuc_RPF_2, CD34_shLuc_RNA_1, CD34_shLuc_RNA_2)
```

Problem 5
---------

**10 points**

Write a code chunk to filter the result from Problem 4 to include only
rows where each of the 12 numerical columns you selected has 50 counts
or more and reassign back to `data`. This is a simple way to avoid genes
that have very low counts. You might be tempted to do this step
separately for each of the 12 columns, but you will receive 5 bonus
points if you instead use the `filter_if` and `all_vars` functions you
learned above.

``` r
data <-data %>%
  filter_if(is.numeric, all_vars(. >= 50)) %>%
  print()
```

    ## # A tibble: 4,239 x 13
    ##    ensembl_gene_id CD34_shRPL5_RPF… CD34_shRPL5_RPF… CD34_shRPL5_RNA…
    ##    <chr>                      <dbl>            <dbl>            <dbl>
    ##  1 ENSG00000000419              101              249             1116
    ##  2 ENSG00000001036              182              295             1487
    ##  3 ENSG00000001084              134              275             1036
    ##  4 ENSG00000001497              253              367             1436
    ##  5 ENSG00000002549              285              447             1228
    ##  6 ENSG00000002586              260              395             2746
    ##  7 ENSG00000002834              254              412             4346
    ##  8 ENSG00000003056              321              698             1379
    ##  9 ENSG00000003393               84              130              832
    ## 10 ENSG00000003402               95              188             1836
    ## # … with 4,229 more rows, and 9 more variables: CD34_shRPL5_RNA_2 <dbl>,
    ## #   CD34_shRPS19_RPF_1 <dbl>, CD34_shRPS19_RPF_2 <dbl>,
    ## #   CD34_shRPS19_RNA_1 <dbl>, CD34_shRPS19_RNA_2 <dbl>, CD34_shLuc_RPF_1 <dbl>,
    ## #   CD34_shLuc_RPF_2 <dbl>, CD34_shLuc_RNA_1 <dbl>, CD34_shLuc_RNA_2 <dbl>

``` r
#write_csv(data, "hw_6_file2.tsv") 
```

Problem 6
---------

**10 points**

Write a code chunk to divide each of the 12 numerical columns by the
corresponding median value for each column and reassign back to `data`.
This median normalization is typically done in high-throughput
experiments after filtering to normalize for sample-to-sample difference
in read depth. Again, you can write lot less code if you use the
`mutate_if` and `funs` functions you learned above.

``` r
data <-data %>%
  #filter_if(is.numeric, all_vars(. >= 50)) %>%
  mutate_if(is.numeric, funs(./median(.))) %>%
  print()
```

    ## Warning: `funs()` is deprecated as of dplyr 0.8.0.
    ## Please use a list of either functions or lambdas: 
    ## 
    ##   # Simple named list: 
    ##   list(mean = mean, median = median)
    ## 
    ##   # Auto named with `tibble::lst()`: 
    ##   tibble::lst(mean, median)
    ## 
    ##   # Using lambdas
    ##   list(~ mean(., trim = .2), ~ median(., na.rm = TRUE))
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_warnings()` to see where this warning was generated.

    ## # A tibble: 4,239 x 13
    ##    ensembl_gene_id CD34_shRPL5_RPF… CD34_shRPL5_RPF… CD34_shRPL5_RNA…
    ##    <chr>                      <dbl>            <dbl>            <dbl>
    ##  1 ENSG00000000419            0.620            0.896            0.817
    ##  2 ENSG00000001036            1.12             1.06             1.09 
    ##  3 ENSG00000001084            0.822            0.989            0.758
    ##  4 ENSG00000001497            1.55             1.32             1.05 
    ##  5 ENSG00000002549            1.75             1.61             0.899
    ##  6 ENSG00000002586            1.60             1.42             2.01 
    ##  7 ENSG00000002834            1.56             1.48             3.18 
    ##  8 ENSG00000003056            1.97             2.51             1.01 
    ##  9 ENSG00000003393            0.515            0.468            0.609
    ## 10 ENSG00000003402            0.583            0.676            1.34 
    ## # … with 4,229 more rows, and 9 more variables: CD34_shRPL5_RNA_2 <dbl>,
    ## #   CD34_shRPS19_RPF_1 <dbl>, CD34_shRPS19_RPF_2 <dbl>,
    ## #   CD34_shRPS19_RNA_1 <dbl>, CD34_shRPS19_RNA_2 <dbl>, CD34_shLuc_RPF_1 <dbl>,
    ## #   CD34_shLuc_RPF_2 <dbl>, CD34_shLuc_RNA_1 <dbl>, CD34_shLuc_RNA_2 <dbl>

\# mutate( CD34\_shRPL5\_RPF\_1 =
CD34\_shRPL5\_RPF\_1/median(CD34\_shRPL5\_RPF\_1), \#
CD34\_shRPL5\_RPF\_2=CD34\_shRPL5\_RPF\_2/median(CD34\_shRPL5\_RPF\_2),
\#
CD34\_shRPL5\_RNA\_1=CD34\_shRPL5\_RNA\_1/median(CD34\_shRPL5\_RNA\_1),
\#
CD34\_shRPL5\_RNA\_2=CD34\_shRPL5\_RNA\_2/median(CD34\_shRPL5\_RNA\_2),
\#
CD34\_shRPS19\_RPF\_1=CD34\_shRPS19\_RPF\_1/median(CD34\_shRPS19\_RPF\_1),
\#
CD34\_shRPS19\_RPF\_2=CD34\_shRPS19\_RPF\_2/median(CD34\_shRPS19\_RPF\_2),
\#
CD34\_shRPS19\_RNA\_1=CD34\_shRPS19\_RNA\_1/median(CD34\_shRPS19\_RNA\_1),
\# CD34\_shRPS19\_RNA\_2=
CD34\_shRPS19\_RNA\_2/median(CD34\_shRPS19\_RNA\_2), \#
CD34\_shLuc\_RPF\_1=CD34\_shLuc\_RPF\_1/median(CD34\_shLuc\_RPF\_1), \#
CD34\_shLuc\_RPF\_2=CD34\_shLuc\_RPF\_2/median(CD34\_shLuc\_RPF\_2), \#
CD34\_shLuc\_RNA\_1=CD34\_shLuc\_RNA\_1/median(CD34\_shLuc\_RNA\_1), \#
CD34\_shLuc\_RNA\_2=CD34\_shLuc\_RNA\_2/median(CD34\_shLuc\_RNA\_2) \#
)%&gt;%

Problem 7
---------

**10 points**

After we do the above filtering and median-normalization, let us
calculate translation efficiency as the average ratio of the RPF and RNA
reads for each treatment condition. Then we calculate how this
translation efficiency changes between target (`rpl5` and `rps19`) and
control (`luc`) shRNAs.

The code implementing the above steps is shown below, but it has a few
errors. Correct them.

``` r
library(tidyverse)
library(tibble)
library(tidyr)
library(readr)
library(ggplot2)
lfc <- data %>%
  mutate(mean_rpl5_te = ((CD34_shRPL5_RPF_1 + CD34_shRPL5_RPF_2) /
                            (CD34_shRPL5_RNA_1 + CD34_shRPL5_RNA_2)) )%>%
  mutate(mean_rps19_te = ((CD34_shRPS19_RPF_1 + CD34_shRPS19_RPF_2) /
                            (CD34_shRPS19_RNA_1 + CD34_shRPS19_RNA_2)) )%>%
  mutate(mean_shluc_te = ((CD34_shLuc_RPF_1 + CD34_shLuc_RPF_2) /
                            (CD34_shLuc_RNA_1 + CD34_shLuc_RNA_2))) %>%

  select(ensembl_gene_id, mean_rpl5_te, mean_rps19_te, mean_shluc_te) %>%
  mutate(lfc_te_rpl5 = log2(mean_rpl5_te / mean_shluc_te),
         lfc_te_rps19 = log2(mean_rps19_te / mean_shluc_te)) %>%
  print()
```

    ## # A tibble: 4,239 x 6
    ##    ensembl_gene_id mean_rpl5_te mean_rps19_te mean_shluc_te lfc_te_rpl5
    ##    <chr>                  <dbl>         <dbl>         <dbl>       <dbl>
    ##  1 ENSG00000000419        0.919         1.49          1.08       -0.239
    ##  2 ENSG00000001036        1.17          1.11          1.45       -0.316
    ##  3 ENSG00000001084        1.02          1.14          0.853       0.258
    ##  4 ENSG00000001497        1.38          1.04          1.75       -0.338
    ##  5 ENSG00000002549        1.78          1.87          1.50        0.245
    ##  6 ENSG00000002586        0.903         0.825         1.14       -0.331
    ##  7 ENSG00000002834        0.479         0.394         0.519      -0.115
    ##  8 ENSG00000003056        1.87          1.87          1.02        0.882
    ##  9 ENSG00000003393        0.831         1.20          0.462       0.847
    ## 10 ENSG00000003402        0.505         0.427         0.344       0.552
    ## # … with 4,229 more rows, and 1 more variable: lfc_te_rps19 <dbl>

``` r
#write_csv(lfc, "hw_6_file_problem7.tsv") 
```

Problem 8
---------

**10 points**

Write code that will create a new dataframe called `mean_lfc` from `lfc`
containing a new column called `avg_lfc`. `avg_lfc` should be the
average of the log2 fold-change in TE (`lfc_te`) upon knockdown of RPL5
and RPS19.

Then select only the gene id column and the new column that you just
created (this will be your new dataframe `mean_lfc`).

``` r
mean_lfc <-lfc %>%
  mutate(avg_lfc =((lfc_te_rpl5+lfc_te_rps19)/2) ) %>%
  select(ensembl_gene_id, avg_lfc ) %>%
  print()
```

    ## # A tibble: 4,239 x 2
    ##    ensembl_gene_id avg_lfc
    ##    <chr>             <dbl>
    ##  1 ENSG00000000419   0.110
    ##  2 ENSG00000001036  -0.355
    ##  3 ENSG00000001084   0.337
    ##  4 ENSG00000001497  -0.543
    ##  5 ENSG00000002549   0.280
    ##  6 ENSG00000002586  -0.396
    ##  7 ENSG00000002834  -0.256
    ##  8 ENSG00000003056   0.880
    ##  9 ENSG00000003393   1.11 
    ## 10 ENSG00000003402   0.431
    ## # … with 4,229 more rows

Problem 9
---------

**10 points**

Write code to join the `mean_lfc` dataframe with the `annotations`
dataframe created at the top of the document and assign back to
`mean_lfc`.

``` r
mean_lfc <- mean_lfc %>%
  left_join(annotations, by = "ensembl_gene_id") %>% 
  print()
```

    ## # A tibble: 4,239 x 6
    ##    ensembl_gene_id avg_lfc symbol name         gene_family        ccds_id       
    ##    <chr>             <dbl> <chr>  <chr>        <chr>              <chr>         
    ##  1 ENSG00000000419   0.110 DPM1   dolichyl-ph… Glycosyltransfera… CCDS82628|CCD…
    ##  2 ENSG00000001036  -0.355 FUCA2  alpha-L-fuc… Alpha-L-fucosidas… CCDS5200      
    ##  3 ENSG00000001084   0.337 GCLC   glutamate-c… <NA>               CCDS4952|CCDS…
    ##  4 ENSG00000001497  -0.543 LAS1L  LAS1 like r… 5FMC ribosome bio… CCDS55433|CCD…
    ##  5 ENSG00000002549   0.280 LAP3   leucine ami… Aminopeptidases    CCDS3422      
    ##  6 ENSG00000002586  -0.396 CD99   CD99 molecu… Blood group antig… CCDS14119|CCD…
    ##  7 ENSG00000002834  -0.256 LASP1  LIM and SH3… LIM domain contai… CCDS62164|CCD…
    ##  8 ENSG00000003056   0.880 M6PR   mannose-6-p… MRH domain contai… CCDS8598|CCDS…
    ##  9 ENSG00000003393   1.11  ALS2   alsin Rho g… Dbl family Rho GE… CCDS46492|CCD…
    ## 10 ENSG00000003402   0.431 CFLAR  CASP8 and F… Receptor ligands|… CCDS56157|CCD…
    ## # … with 4,229 more rows

``` r
#or full_join()
```

Problem 10
----------

**10 points**

1.  Write code to select only the bottom 10 genes with the lowest
    `avg_lfc` and display the gene `symbol`, gene `name` and `avg_lfc`
    for these genes.
2.  Create a figure using ggplot to visualize these results. Write a few
    sentences to justify the choices you made when creating your figure.

``` r
mean_lfc %>%
  #group_by(ensembl_gene_id) %>%
  select("name", "symbol", "avg_lfc")%>%
  arrange(avg_lfc) %>%
  slice(0:10)%>%
  print()%>%
  ggplot(aes(x = symbol, y = avg_lfc, label= round(avg_lfc, 2) )) +
  geom_point() +
  geom_text( hjust = 0, nudge_y = 0.1, nudge_x = -0.1,  size=5)+
  theme_classic()+
  scale_y_continuous(limit= c(-3,-1)) +
  
  labs(x = "Gene symbol", y= "Average of the log2 fold-change in TE", size=5)
```

    ## # A tibble: 10 x 3
    ##    name                                       symbol avg_lfc
    ##    <chr>                                      <chr>    <dbl>
    ##  1 H2A clustered histone 6                    H2AC6    -2.95
    ##  2 H2B clustered histone 12                   H2BC12   -2.79
    ##  3 ribosomal protein S15                      RPS15    -2.27
    ##  4 cytochrome c oxidase subunit 8A            COX8A    -2.02
    ##  5 ribosomal protein L18a                     RPL18A   -2.01
    ##  6 ribosomal protein lateral stalk subunit P1 RPLP1    -2.01
    ##  7 H2A.X variant histone                      H2AX     -1.86
    ##  8 ribosomal protein S26                      RPS26    -1.85
    ##  9 apolipoprotein E                           APOE     -1.68
    ## 10 ribosomal protein L7a                      RPL7A    -1.68

![](README2_files/figure-markdown_github/unnamed-chunk-11-1.png)

``` r
 #print("name", "symbol", "avg_lfc" )

'Explanation of figure: I chose to use `theme_classic()` becuase I wanted to remove the grey background and just have a white background. I adjusted the y-axis with `scale_y_continuous` in order to  make the position of the data slightly more visually appealing. I used `geom_text` to label each data point with the gene symbol. I modified the label so the text is slightly to the right of the data point. I chose to use `geom_point` because `geom_hist` might have had overlap. With `geom_point`, I could show the discrete data points. '
```

    ## [1] "Explanation of figure: I chose to use `theme_classic()` becuase I wanted to remove the grey background and just have a white background. I adjusted the y-axis with `scale_y_continuous` in order to  make the position of the data slightly more visually appealing. I used `geom_text` to label each data point with the gene symbol. I modified the label so the text is slightly to the right of the data point. I chose to use `geom_point` because `geom_hist` might have had overlap. With `geom_point`, I could show the discrete data points. "

``` r
  #filter(min_rank(avg_lfc)<= 10)
```

**When you are satisfied with your code and answers, use the “Knit”
button in RStudio to create the final set of files. Save the result as a
PDF and and submit it.**
