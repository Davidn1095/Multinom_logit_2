# Multinom_logit_2

The script involves fitting, evaluating, and comparing multinomial logistic regression models, performing predictions, and conducting model selection to find the most suitable model for the data.

### Factor Creation and Releveling:

- `Chapman.Cuali$Presion <- factor(Chapman.Cuali$Presion, levels = c("Optima", "Normal", "Alta", "Descompensada"))`: Converts the `Presion` column in the `Chapman.Cuali` DataFrame into a factor with the specified order of levels.
- `Chapman.Cuali$IMC <- factor(Chapman.Cuali$IMC, levels = c("Normal", "Sobrepeso", "Obesidad"))`: Converts the `IMC` column into a factor with the specified levels.

### Fitting Multinomial Logistic Regression:

- `Ajuste.Multinom.Cuanli <- multinom(Presion ~ Edad + Colesterol + IMC, data = Chapman.Cuali)`: Fits a multinomial logistic regression model with `Presion` as the response variable and `Edad`, `Colesterol`, and `IMC` as predictors.

### Model Summary and Exponentiated Coefficients:

- `summary(Ajuste.Multinom.Cuanli)`: Provides a summary of the fitted multinomial logistic regression model.
- `exp(summary(Ajuste.Multinom.Cuanli)$coefficients)`: Exponentiates the model's coefficients to interpret them as odds ratios.

### Model Comparison Using ANOVA:

- `anova(multinom(Presion ~ Edad + Colesterol + IMC, data = Chapman.Cuali), multinom(Presion ~ Edad + Colesterol, data = Chapman.Cuali))`: Compares two multinomial logistic regression models with different sets of predictors using ANOVA to test if the additional predictors significantly improve the model.

### Confidence Intervals for Model Parameters:

- `exp(confint(Ajuste.Multinom.Cuanli))`: Calculates and exponentiates the confidence intervals for the parameters of the multinomial model.

### Predictions from the Model:

- `predict(Ajuste.Multinom.Cuanli, type = "probs")[1:10,]`: Predicts the probabilities for the first 10 observations in the dataset.
- `predict(Ajuste.Multinom.Cuanli, type = "class")[1:10]`: Predicts the class for the first 10 observations.

### Contingency Table for Actual vs Predicted Classes:

- `table(Chapman.Cuali$Presion, predict(Ajuste.Multinom.Cuanli, type = "class"))`: Creates a contingency table comparing the actual `Presion` levels with those predicted by the model.

### Model Deviance and Significance Testing:

- `pchisq(Ajuste.Multinom.Cuanli$deviance, 585, lower.tail = F)`: Calculates the p-value for the deviance of the model to test its overall significance. The value 585 should be the degrees of freedom.

### Fitting a Null Multinomial Logistic Regression Model:

- `Ajuste.Multinom.0 <- multinom(Presion ~ 1, data = Chapman.Cuali)`: Fits a multinomial logistic regression model with only an intercept (null model).

### Stepwise Model Selection:

- `Ajuste.Multinom.Step <- step(Ajuste.Multinom.0, scope = list(lower = Presion ~ 1, upper = Presion ~ Edad + Colesterol + IMC), direction = "both")`: Performs stepwise model selection starting from the null model. The function iteratively adds or removes predictors within the specified scope to find an optimal model.
- `summary(Ajuste.Multinom.Step)`: Provides a summary of the stepwise-selected multinomial logistic regression model.

