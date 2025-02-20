# Chicago Housing Analysis and Anorexic Patients Statistical Study

## Overview
This R script performs statistical analysis on two datasets: **Chicago Housing Income** and **Anorexic Patients' Weight Changes**. The study applies **descriptive statistics, confidence interval estimation, and hypothesis testing** using R.

## Key Features
- **Chicago Housing Analysis**:
  - Reads and processes income data from Chicago public housing residents.
  - Generates a **histogram** to visualize income distribution.
  - Computes **mean and standard deviation** of household income.
  - Calculates a **95% confidence interval** for mean income.

- **Anorexia Patients Analysis**:
  - Compares pre- and post-therapy weight changes in anorexic patients.
  - Uses **boxplots** to visualize weight differences.
  - Performs a **t-test** to compare weight changes between therapy and control groups.
  - Computes a **95% confidence interval** for treatment effect.

## Installation
Ensure you have R and required packages installed:
```r
install.packages("ggplot2")
install.packages("arules")
```

## Usage
### Chicago Housing Analysis
```r
chicago_R_data <- read.table("C:/Users/kabir/OneDrive/Documents/Chicago.dat.txt", header=TRUE, sep="")

hist(chicago_R_data$income, main="Histogram of Annual Income for Chicago Residents (Public Housing)",
     xlab="Resident Income (in thousands)", ylab="Frequency", col="sky blue", cex.main=0.8)

mean_ChicagoUS_income <- mean(chicago_R_data$income)
sd_ChicagoUS_income <- sd(chicago_R_data$income)    

print(paste("Mean Income:", mean_ChicagoUS_income))
print(paste("Standard Deviation of Income:", sd_ChicagoUS_income))

t_conf_interval_ChicagoUS <- t.test(chicago_R_data$income, conf.level=0.95)
ci <- t_conf_interval_ChicagoUS$conf.int

cat("The 95% Confidence Interval for mean income in Chicago is:", ci[1], "to", ci[2], "\n")
```

### Anorexic Patients Weight Analysis
```r
anorexiapatient_data <- read.table("C:/Users/kabir/OneDrive/Documents/Anorexia.dat.txt", header=TRUE, sep="")

Anorexia_family_therapy_data <- subset(anorexiapatient_data, therapy == "f")
summary(Anorexia_family_therapy_data$before)
summary(Anorexia_family_therapy_data$after)

boxplot(Anorexia_family_therapy_data$before, Anorexia_family_therapy_data$after,
        names = c("Before", "After"), main = "Family Therapy Weight Changes (Girls)",
        col=c("Sky blue", "Ivory"), cex.main=0.8)

anorexiapatient_data$weight_change <- anorexiapatient_data$after - anorexiapatient_data$before

Anorexiafamily_therapy <- anorexiapatient_data[anorexiapatient_data$therapy == 'f', 'weight_change']
Anorexiacontrol_group <- anorexiapatient_data[anorexiapatient_data$therapy == 'c', 'weight_change']

t_test_result <- t.test(Anorexiafamily_therapy, Anorexiacontrol_group, conf.level=0.95)
Anorexiapatients_Confidence <- t_test_result$conf.int

print(Anorexiapatients_Confidence)
```

## Results
### **Chicago Housing Income Analysis**
- **Mean Annual Income:** $20,333
- **Standard Deviation:** $3,681
- **95% Confidence Interval for Mean Income:** $18,959 - $21,708
- The **income distribution is right-skewed**, indicating more lower-income households.

### **Anorexia Patients Analysis**
- **Mean Pre-Therapy Weight:** ~83.23 kg
- **Mean Post-Therapy Weight:** ~90.49 kg
- **Treatment Effect Confidence Interval:** 2.98 to 12.45 kg weight increase
- The results indicate a **significant weight gain** after therapy compared to the control group.

## Visualization
- **Histograms** to illustrate income distribution.
- **Boxplots** to compare pre- and post-therapy weight changes.

## References
- Favero, L. P., & Belfiore, P. (2019). *Data Science for Business and Decision Making*. Elsevier S & T.
- Grolemund, G., & Wickham, H. (2017). *R for Data Science*. O’Reilly Media.
- Thulin, M. (2021). *Modern Statistics with R*. Eos Chasma Press.

