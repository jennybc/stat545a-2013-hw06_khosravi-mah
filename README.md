HW #06: The Last Challenge
--------------------------

Here is a description of how this pipeline works and what it does. The source data from last week,
i.e. "Bank Profitability Statistics" under the "Finance" subsection from [OECD.Stat Extracts](http://stats.oecd.org/)
was imported again, but a better sence of cleaning and managing the data set was applied this time.  

### Data Description:  

The quantitative values of different financial indexes, in different types of banking institutions, are presented
for 33 countries in a ten year time span. Variables in the cleaned data are country, bank (commercial vs. saving,
etc.), index (interest income, provisions, loans, etc.), year, and finally values.

### Files edited or added after the deadline

 - Edited: `Readme.md`; This Readme file was first submitted on due date and edited the day shown here.
 - Added: [`Actual_Makefile`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Actual_Makefile); I tried to write an actual make file by introducing this file to get to the next level and use it to make htmls in makefile, but, unfortunately, I could not succeed to run this in PowerShell. I installed GNU make, MinGW, and MSYS, and I went through documentations on these and also on PowerShell, but I could not figure the problem out. I changed the `ExecutionPolicy` to `RemoteSigned` in PowerShell and added the paths of `make` to "Windows Path", but still I get the same error. I only know that the error is associated with PowerSehll by trying Jenny's template case, this is what I see: [Error Figure](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/PowerShell_make_error.png). Song and I had some discussions on this and tried some different probable solutions but they did not work and I finally gave up!

### How to replicate my analysis:

  * Essential tools:
    - Input data: [`BankProfitabilityStatistics.csv`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/BankProfitabilityStatistics.csv). You should view it in raw version, unfortunately. GitHub doesn't show big files like this one!
    - Scripts: [`Cleaning_and_Ordering.R`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Cleaning_and_Ordering.R) and [`Aggregate_and_Plots.R`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Aggregate_and_Plots.R)
    - Makefile-like script: [`Make.R`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Make.R)
  * `Source` the `Makefile.R` in RStudio, or alternatively, in a shell: `Rscript Makefile.R`.
  * When you run the code, you will see a number of warnings which are addressing the *missing values*. This the result of missing data (NAs) in the raw data set.
  
### Results:

New files you should see after running the pipeline and a short elaboration on each of them is presented here.
I have made a [`My_figures`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/tree/master/My_figures) 
folder here just to make the homework repository a bit tidier:

  * #### Outputs of [`Cleaning_and_Ordering.R`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Cleaning_and_Ordering.R):
    - [`Barchart_income_types.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Barchart_income_types.png):
     * Shows and compares two income types in different banks.
     ![](https://raw.github.com/jennybc/stat545a-2013-hw06_khosravi-mah/master/My_figures/Barchart_income_types.png)
    - [`Density_NetProvisions.png `](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Density_NetProvisions.png):
     * Shows density diagram for net provision index in different countries. We can see from this figure that data for some countries like *Portugal* and *Turkey* is confined to a relatively small range inceasing their corresponding height in density diagram.
     ![](https://raw.github.com/jennybc/stat545a-2013-hw06_khosravi-mah/master/My_figures/Density_NetProvisions.png)
    - [`Expense_boxplot.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Expense_boxplot.png):
     * We can see from this figure that range of data for *Korea* is much higher comparing to other countries. Also, again we can notice that data for some countries like *Portugal*, *Norway*,*Turkey* is confined to a relatively small range.
    - [`finance_clean.tsv`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/finance_clean.tsv)
     * This is the clean version of the input data. Actually,its `.rds` version (`finance_clean.rds`) is read in the second script to preserve the orders.
    - [`finance_wide.tsv`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/finance_wide.tsv)
     * This is the reshaped to wide version of the `finance_clean.tsv`, which is produced to perform data aggregations and make plots on different indexes that are basically different levels of `finance_clean.tsv`. The other difference is that dependant bank types, e.g. *All_banks*, are omitted here.

  * #### Outputs of [`Aggregate_and_Plots.R`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/Aggregate_and_Plots.R):
  * Loans in all banks:
    - [`Loans_allBanks_selectedCountries_Actual.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Loans_allBanks_selectedCountries_Actual.png):
     * we can see increase in loans in different years in this figure. Average changes are different in order, and logging also fades away the incease in years. So comparing the average changes, which is done in the next figure, is the other option two just study the countries' relative performance.
    - [`Loans_allBanks_selectedCountries_Normalized.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Loans_allBanks_selectedCountries_Normalized.png):
     * Now this is much better. In the next figure, I have put the last two figures side by side in a `.pdf` figure file.
    - [`Loans_allBanks_selectedCountries_NormalizedVsActual.pdf`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Loans_allBanks_selectedCountries_NormalizedVsActual.pdf):
     * I know! unfortunately GitHub shows it only in raw view. I couldn't find a good way to make a `.png` out of it!
    - [`Loans_allBanks_allCountries_Normalized.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Loans_allBanks_allCountries_Normalized.png):
     * Not interesting! A better way to study this is to make regressions and compare them:
    - [`LoansSlopes_allBanks_allCountries_Normalized.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/LoansSlopes_allBanks_allCountries_Normalized.png):
     * Slopes of linear regressions of normalized data is ordered and plotted here. The table of the coefficients is also written to file next: 
    - [`LoansVsYear_lmCoefficients.tsv`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/LoansVsYear_lmCoefficients.tsv):
     * This is table of the coefficients of linear regressions of normalized data. We can compare intercepts as well:
    - [`LoansCoefs_allBanks_allCountries_Normalized.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/LoansCoefs_allBanks_allCountries_Normalized.png):
     * Well, given that we have devided data for each year by its mean to normalize, countries with higher slope would have lower intercepts accordingly. So, it is better to compare these coefficients for actuall data:
    - [`LoansCoefs_allBanks_allCountries_Actual.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/LoansCoefs_allBanks_allCountries_Actual.png):
     * Now this seems to be more informative and a more rational way to compare linear regression coefficients. Note that intercepts for *Russia*, *Estony* and *Slovenia* are negative and not plotted here. Ditto *Japan*'s Slope.
  * Different banks and indexes:
    - [`IndexCorrelation_interest_provisions.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/IndexCorrelation_interest_provisions.png):
     * Correlation of different indexes (`Net_provisions` and `Interest_income` here) can be invesigated using the produced wide data ([`finance_wide.tsv`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/finance_wide.tsv)).
    - [`IndexCorrelation_interest_provisions_facet.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/IndexCorrelation_interest_provisions_facet.png):
     * This is the faceted bubble diagram of the previous figure, for a selection of countries and sized by loans:
    - [`Employment_CommercialBanks_SelectedCounttries.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Employment_CommercialBanks_SelectedCounttries.png):
     * This figure and the next one give us some information about employment in different banking institutes (sized by number of institutions) in the first decade of 20th century. We can see here that some countries show a decrease in emplyees between 2002 to 2006. Also, after 2007 another decrease in the employee numbers, or at least a decrease in the slope, occurs. 
    - [`Employment_CommercialBanks_USA.png`](https://github.com/Mahdiark/stat545a-2013-hw06_khosravi-mah/blob/master/My_figures/Employment_CommercialBanks_USA.png):
     * This figure on the other hand, shows that in United States decrease in emplyees for commercial banks happens after 2007 with decrease in number of institutions. These last two figures imply that something global has happened after 2007 that might be worth studying.
