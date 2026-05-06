
# Introduction + Question

The data used in this analysis comes from the [`wildfire` dataset](https://r-packages.io/datasets/wildfire) included in the `DATAstudio` package in R. This dataset compiles records of wildfire events in Portugal, showing the amount of area burned (in hectares) for wildfires in Portugal, and then accompanied by Canadian Forest Fire Weather Index System Indices (CFFWIS). This data was originally collected from the monitoring systems and environmental observation networks. The goal for this project is to investigate how environmental factors influence wildfire behavior, specifically focusing on burned area. 

Each row in this dataset represents a day. The dataset includes a primary response variable, `burnt_area`, which represents the total area burned per day. Since this data is taken on a national level, the analysis focuses on large-scale environmental influences on wildfire activity, rather than individual fire events.  

The dataset also includes predictor variables that influence and describe fire weather and fuel conditions:

| Column | Meaning |
|---|---|
| Burnt Area (`burnt_area`) | Daily burnt area in hectares |
| Fire Weather Index (`fwi`) | Numeric rating of fire intensity |
| Buildup Index (`bui`) | Numeric rating of fuel available for combustion |
| Initial Spread Index (`isi`) | Numeric rating of expected rate of fire spread |
| Fine Fuel Moisture Code (`ffmc`) | Numeric rating of moisture content of litter and other fuels |
| Daily Severity Rating (`dsr`) | Numeric rating of difficulty to control fires |
| Duff Moisture Code (`dmc`) | Numeric rating of average moisture content of loose compact organic layers |
| Drought Code (`dc`) | Rating of average moisture content of compact organic layers |
|`day`, `month`, `year` | Time stamp for each point |

I investigated the influence chosen predictor variables had on the response variable, and developed the research questions: How do environmental conditions influence the daily total burned area at the national scale?



# Methods

For my analysis, I chose one response variable (`burnt_area`)  and four predictor variables ( `fwi`, `isi`, `bui`, `dc`). Once I cleaned up my data and filtered out incorrect column identification (capital variables) and NA points, I divided the data into two categories: days with fire and days without fire (1 or 0). Given the number of zeros, this justifies transforming the data to make it work with normal tests. I started with some initial plots to see how the data works with modeling. The initial plot was extremely right-skewed (positively skewed), meaning I couldn’t simply use normal testing in its original form, which explains the need to transform the data from the few extreme fire days within the dataset. 

I used log scaling to better center the data, since it handles zeros and mitigates skew. Once I log-scaled the dataset, I created simple line regression plots to determine the relationship between each of the predictor variables and the response variable to see clear positive trends (a more linear relationship), which supports regression modeling. Meaning that when the predictor variable increases, so does the response variable. From exploratory data analysis, I moved on to some exploratory plots with some of the predictor variables, which answered some comparison group inquiries:

Comparison Groups: High vs. low fire risk days (`fwi`)
High vs. low fuel availability (`bui`)
Seasonal comparisons ( `month`)

After answering the initial questions, I moved onto statiscal testing to make the plot results more reliable and initiate some hypothesis testing:

$H_0$: Burnt area has no significant relationship with FWI, ISI, BUI, and DC
$H_A$: Burnt area has a significant relationship with at least one of FWI, ISI, BUI, and DC

I performed a t-test and summarized a model of all variables to extract the p-value, mean, confidence interval (CI), and R-squared (R2) value. Finally, to validate the earlier regression modeling, I created a four-plot residual vs. fitted values model to accurately assess the reliability of the data. Additionally, I created my own residual plot to test the four-plot model's accuracy. 


# Results

Wildfire activity varied across environmental conditions. We see variability through the months, with a peak wildfire count in August and the months leading up to and following it. This suggests that summertime in Portugal harbors the influential conditions for wildfires. Comparisons between grouped variables further support this pattern. Days classified as high fire risk based on `fwi` had significantly higher rates of area burned. We can see a similar trend with `bui`, with high rates increasing the area burned; the area burned is influenced by the amount of fuel available. 

The 95% CI does NOT include 0, meaning the wildfire activity is statistically meaningful and has a strong relationship with the predictor variables chosen. The combined model explores the overall effects of each environmental response variable. The R-squared value of 0.72 explains that 72% of the wildfire variability is explained by environmental conditions. This, however, does mean that the model leaves 28% unexplained. The 2.2e-16 p-value means we reject our null hypothesis, which explains that burnt area has a significant relationship with at least one of fwi, isi, bui, and dc.



The residual modeling suggests that the linear regression classification is accurate and reliable:

Residuals vs Fitted is scattered around 0, which tells us that the model is appropriate and linear.
Q-Q Residuals follow a straight line, indicating that the residuals follow a normal distribution.
Scale-Location has a random spread of points, which indicates constant variance (homoscedasticity).
Residuals vs Leverage has a few points that outlay Cook's distance lines, which means they are highly influential and have the opportunity to disproportionately affect the regression results. 

My own residual plot agrees with the other modeled residual plot, proving accuracy and consistent results. 


# Interpretation + Limitations

These results indicate that environmental conditions play a significant role in determining wildfire severity at the national scale in Portugal. The inclusion of `fwi` and `bui` shows a particular influence, showcasing the importance of atmospheric and ecological factors in wildfire analysis. 

One limitation within this dataset was the lack of temperature values to accompany the scaled values given by each variable. Although the dataset was still interpretable with the available scaled variables, the lack of actual temperature (and wind speed)  that goes with each of these data points is not included. I think the inclusion of temperature and perhaps wind speed would have made the data more digestible and improved the accuracy of the modeling. 


# Conclusion

Wildfires have conditions in which they happen, but they also have various variables that influence the amount of area they burn. There is clear evidence that supports the influence of each variable tested on the area burned. With the increasing of each predictor variable, we see a strong correlation with the response variable; as each predictor variable increases, so does the response variable. This can be proved through log-transformed regression plotting, residual modeling, and t-testing. Though many days did not experience fires, those that did showed a direct, strong relationship with `fwi`, `isi`, `bui`, and `dc`.

# References

Lee, M. W., de Carvalho, M., Paulin, D., Pereira, S., Trigo, R., and da Camara, C. (2026). BLAST: A Bayesian lasso tail index regression model with an application to extreme wildfires. Submitted.
