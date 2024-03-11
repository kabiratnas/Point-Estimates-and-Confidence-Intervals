# Point-Estimates-and-Confidence-Intervals
Descriptive Statistics Estimates and Confidence Intervals for Chicago Public Housing Analysis
Code
chicago_R_data <- read.table("C:/UsersChicago.dat.txt", header=TRUE, sep="")
hist(chicago_R_data$income, main="Histogram of Annual Income for Chicago Residents (Public Housing)", xlab="Resident Income (in thousands)", ylab="Frequency", col="sky blue", cex.main=0.8)
mean_ChicagoUS_income <- mean(chicago_R_data$income)
sd_ChicagoUS_income <- sd(chicago_R_data$income)    
print(paste("Mean Income:", mean_ChicagoUS_income))
print(paste("Standard Deviation of Income:",sd_ChicagoUS_income))
t_conf_interval_ChicagoUS <- t.test(chicago_R_data$income, conf.level=0.95)
t_conf_interval_ChicagoUS
ci <- t_conf_interval_ChicagoUS$conf.int
cat("The 95% Confidence Interval for mean income in Chicago is:", ci[1], "to", ci[2], "\n")


Results
> chicago_R_data <- read.table("C:/Users/kabir/OneDrive/Documents/Chicago.dat.txt", header=TRUE, sep="")
> hist(chicago_R_data$income, main="Histogram of Annual Income for Chicago Residents (Public Housing)", xlab="Resident Income (in thousands)", ylab="Frequency", col="sky blue", cex.main=0.8)
> 
> 
> mean_ChicagoUS_income <- mean(chicago_R_data$income)
> sd_ChicagoUS_income <- sd(chicago_R_data$income)    
> print(paste("Mean Income:", mean_ChicagoUS_income))
[1] "Mean Income: 20.3333333333333"
> print(paste("Standard Deviation of Income:",sd_ChicagoUS_income))
[1] "Standard Deviation of Income: 3.68111052708876"
> t_conf_interval_ChicagoUS <- t.test(chicago_R_data$income, conf.level=0.95)
> t_conf_interval_ChicagoUS
	One Sample t-test
data:  chicago_R_data$income
t = 30.255, df = 29, p-value < 2.2e-16
alternative hypothesis: true mean is not equal to 0
95 percent confidence interval:
 18.95878 21.70788
sample estimates:
mean of x 
 20.33333 
> ci <- t_conf_interval_ChicagoUS$conf.int
> cat("The 95% Confidence Interval for mean income in Chicago is:", ci[1], "to", ci[2], "\n")
The 95% Confidence Interval for mean income in Chicago is: 18.95878 to 21.70788 

Figure 1
Histogram Statistics for Public Housing in Chicago
 
The shape of the distribution appears to be right skewed (positively skewed), meaning that there are a greater number of households with incomes on the lower end of the scale and fewer households with higher incomes. This is indicated by the longer tail on the right side of the histogram. 
The average annual income among the 30 sampled households in Chicago public housing is approximately $20,333. This figure represents the central tendency of the income distribution, suggesting that the typical head of household in this sample earns around this amount.
The standard deviation of approximately $3,681 indicates a substantial diversity in household incomes. While some households earn incomes close to the average, others have significantly higher or lower earnings, demonstrating a wide economic disparity within the Chicago public housing community.
The 95% confidence interval, extending from approximately $18,959 to $21,708, should not be mistaken as a reflection of the variation in individual earnings. Instead, it represents a statistical estimate that provides us with 95% confidence in predicting where the actual mean income for all Chicago public housing heads of household would lie, were it feasible to include each one in the study.
Descriptive Statistics Estimates and Confidence Intervals for Anorexic patients Analysis
Code
anorexiapatient_data <- read.table("C:/Users/kabir/OneDrive/Documents/Anorexia.dat.txt", header=TRUE, sep="")
Anorexia_family_therapy_data <- subset(anorexiapatient_data, therapy == "f")
summary(Anorexia_family_therapy_data$before)
summary(Anorexia_family_therapy_data$after)
boxplot(Anorexia_family_therapy_data$before,
        Anorexia_family_therapy_data$after,
        names = c("Before", "After"),
        main = "Family Therapy Weight Changes (Girls)", 
        col=c("Sky blue", "Ivory"),
        cex.main=0.8)
anorexiapatient_data$weight_change <- anorexiapatient_data$after - anorexiapatient_data$before
Anorexiafamily_therapy <- anorexiapatient_data[anorexiapatient_data$therapy == 'f', 'weight_change']
Anorexiacontrol_group <- anorexiapatient_data[anorexiapatient_data$therapy == 'c', 'weight_change']
t_test_result <- t.test(Anorexiafamily_therapy, Anorexiacontrol_group, conf.level=0.95)
Anorexiapatients_Confidence <- t_test_result$conf.int
print(Anorexiapatients_Confidence)
Results
> anorexiapatient_data <- read.table("C:/Users/kabir/OneDrive/Documents/Anorexia.dat.txt", header=TRUE, sep="")
> Anorexia_family_therapy_data <- subset(anorexiapatient_data, therapy == "f")
> 
> summary(Anorexia_family_therapy_data$before)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  73.40   80.50   83.30   83.23   86.00   94.20 
> summary(Anorexia_family_therapy_data$after)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  75.20   90.70   92.50   90.49   95.20  101.60 
> boxplot(Anorexia_family_therapy_data$before,
+         Anorexia_family_therapy_data$after,
+         names = c("Before", "After"),
+         main = "Family Therapy Weight Changes (Girls)", 
+         col=c("Sky blue", "Ivory"),
+         cex.main=0.8)
> 
> anorexiapatient_data$weight_change <- anorexiapatient_data$after - anorexiapatient_data$before
> 
> Anorexiafamily_therapy <- anorexiapatient_data[anorexiapatient_data$therapy == 'f', 'weight_change']
> Anorexiacontrol_group <- anorexiapatient_data[anorexiapatient_data$therapy == 'c', 'weight_change']
> t_test_result <- t.test(Anorexiafamily_therapy, Anorexiacontrol_group, conf.level=0.95)
> Anorexiapatients_Confidence <- t_test_result$conf.int
> print(Anorexiapatients_Confidence)
[1]  2.976597 12.452815
attr(,"conf.level")
[1] 0.95
Figure 2
Histogram Statistics for Public Housing in Chicago

References
Favero, L. P., & Belfiore, P. (2019). Data Science for Business and Decision Making. Elsevier S & T. https://reader2.yuzu.com/books/9780128112175
Grolemund, G., & Wickham, H. (2017). R for Data Science. O’Reilly Media.
Thulin, M. (2021). Modern Statistics with R. Eos Chasma Press. ISBN 9789152701515.

