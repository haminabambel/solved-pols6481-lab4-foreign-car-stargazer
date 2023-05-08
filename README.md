Download Link: https://assignmentchef.com/product/solved-pols6481-lab4-foreign-car-stargazer
<br>
The primary objective is to examine how the error variance is estimated and how the standard errors for the regression coefficients are calculated. A secondary objective is to examine model specification questions, particularly how we balance the costs of <em>under-</em>specification (omitted variable bias) against those of <em>over-</em>specification (irrelevant variable bias and multicollinearity). In so doing, we will explore measures of regression model fit.




<ol>

 <li><strong> Datasets</strong>: <em>caschool.dta</em></li>

</ol>




<strong>III. Packages</strong>:  <em>foreign</em>, <em>car</em>, <em>stargazer</em>




<ol>

 <li><strong> Preparation</strong></li>

</ol>

<ul>

 <li>Open RStudio by double-clicking the icon or selecting RStudio from the Windows Start menu.</li>

 <li>Open the project from the Projects menu</li>

 <li>Pull from Github for any updates</li>

 <li>Navigate in the lower right file area to the Lab 3 section</li>

 <li>5) Open the R script by typing <em>Ctrl</em>+<em>O</em> or by clicking on File in the upper-left corner, using the dropdown menu, and navigating to the script in your working directory.</li>

 <li>Run lines 1–7  in the R script to load three packages that you will need. If any of these are not already installed, you need to install them using the <strong>Packages</strong> tab or with code like in line 3.</li>

</ul>




<ol>

 <li><strong> Instructions for Lab Week 04</strong></li>

</ol>




You will use the same dataset from Lab Week 03, exploring the factors that determine test scores in school districts in California.




Begin by loading the dataset, typing the following line, changing the directory if needed:

cadta&lt;-read.dta(here(“data”,”caschool.dta”))

This command is shown in line 11 of the R script. If you failed to load the <em>foreign</em> package earlier, then R will not load the Stata dataset. If you did not load the <em>here</em> package, you will need to specify the working directory manually and move the file to the correct working directory. Ensure that the package is both installed and loaded, and then re-run the line of code.




Recall that <em>CaliforniaTestScores.pdf</em> lists the variables you will use, and some that you will not. Some key demographic variables are the average income of families in the district, in thousands of dollars (avginc), the percent of students qualifying for the CalWORKs program, which is the state of California’s name for welfare (calw_pct), the percent of students qualifying for reduced-price lunch (meal_pct), and the percent of students who are learning English as a second language (el_pct). Three other potentially influential variables are the number of computers per student (comp_stu), the district’s expenditures per student (expn_stu), and the number of students per teacher (str).




Line 12 changes R Studio’s default to <em>not </em>use scientific notation. If you do not run this line of code, then the first time you run a correlation (line 21) you will –1.79e–15, which is actual –1.79 x 10<sup>–15</sup>, or 0.00000000000000179, or virtually zero. Line 13 changes R Studio’s default to round to three digits for easier examination of the correlation matrix, speaking of which …




Run line 14 to create the <em>correlation</em> matrix for the seven explanatory variables that are listed above; if you look down the first column you can see how each explanatory variable correlates to avginc, which was an important explanatory variable in last week’s lab. You may wish to scan across individual rows or down columns to identify associations that appear particularly strong. For example, variables that measure relative affluence of a district – avginc, calw_pct, and  meal_pct – are associated strongly but not necessarily <em>positively</em>.




If you prefer graphical illustrations of association, run lines 16-17  to display scatterplots of the first four variables (districts’ demographics) and the last three variables (districts’ policies), respectively.




<ol>

 <li><strong><em> Omitted Variable Bias</em></strong></li>

</ol>




Start by running line 19 to estimate a baseline model, which regresses average test scores in a district (testscr) on average income (avginc) and the percent of students who are English-language learners (el_pct).




What is the baseline model’s R<sup>2</sup>? ______ . What is the model’s residual standard error? ______ .




What are the coefficient and standard error for the second variable, el_pct, i.e., the percent of students who are English language learners ( = ______, and <em>se</em>() = ______ ).




Run line 20 to check that the mean residual from the baseline model equals zero, and then run line 21 to check that the residuals are uncorrelated to the <strong>included</strong> variables.




Next, run line 22  to explore whether the residual from the baseline model is related to the two <strong>omitted</strong> measures of affluence: the percent of students whose families qualify for welfare (calw_pct) and the percent of students who qualify for reduced price lunch (meal_pct). If either correlation is sufficiently large then you might consider a variable to be “relevant” and potentially worthy of inclusion in the model’s specification.




Run line 24 to estimate a model that adds the variable calw_pct to the specification; what is this second model’s R<sup>2</sup>? ______ . What is this second model’s residual standard error? ______ .




Write down the values of the coefficient and standard error for el_pct, i.e., the percent of students who are English language learners ( = ______, and <em>se</em>() = ______ ) in this model.




Also write down both the coefficient and standard error for calw_pct, i.e., the percent of students who qualify for welfare ( = ______, and <em>se</em>() = ______ ) for later reference.




Next, run line 26 to estimate a model that adds the variable meal_pct to the specification; what is this third model’s R<sup>2</sup>? ______ . What is this third model’s residual standard error? ______ .




Write down the values of the coefficient and standard error for el_pct, i.e., the percent of students who are English language learners ( = ______, and <em>se</em>() = ______ ) in this model.




Also write down the new coefficient and standard error for calw_pct, i.e., the percent of students who qualify for welfare ( = ______, and <em>se</em>() = ______ ), which was in the second model as well.




You should observe that adding more indicators of affluence improved the model fit, represented by increases in the R<sup>2</sup> and decreases in the residual standard error (a.k.a. <em>sigma</em>). Each time a variable is added, the model gets less noisy, but this has come at a cost. All the variables’ coefficients become smaller (in absolute value) in each successive model, and one variable’s coefficient becomes statistically insignificant when the percent of students who qualify for free meals (meal_pct) is added to the model.




Run line 20 to create a correlation matrix which shows the interrelationships among these four measures of affluence as well as their correlations to districts’ test scores. The variable that we added to the specification last, meal_pct, has the strongest bivariate correlation to test scores and has the strongest correlations to the other variables. If you inspect the equations for the multiple regression coefficients (from lecture), perhaps you can see why adding this variable changes the other coefficients and their standard errors so dramatically.




<ol>

 <li><strong><em> Multicollinearity</em></strong></li>

</ol>




In lecture, we will discuss using the Variance Inflation Factor as a measure of the degree of multicollinearity. Run line 30 (which uses the <em>car</em> package) to calculate VIF’s for each of the variables using the third model we estimated. Which variable has the highest VIF? What was the threshold that Wooldridge asserts we should use as a rule of thumb for deciding whether to drop a variable? What was the justification for using this threshold?




Run line 32 to check how the VIF is calculated for one explanatory variable, meal_pct. The code asks R to regress meal_pct on the other regressors and then find the R<sup>2</sup> of this regression. Fill in your own code in this space to check that the VIF for meal_pct equals 1/(1-R<sup>2</sup>):

&gt;




Suppose we decided to drop calw_pct from the specification, because it was statistically insignificant in the last regression. For instance, you can run line 34 to estimate the “final” model:

&gt; final &lt;- lm(testscr ~ avginc + el_pct + meal_pct, cadta)




How does this final model’s fit (R<sup>2</sup> = _____ ) compare to the third model (from line 26)?

How does this model’s residual standard error (<em>sigma </em>= _____ ) compare to the third model?

You can also re-check the variance inflation factors, as shown in line 35:

&gt; vif(final)




If you were advising another student about a potential multicollinearity problem in their research, what would seem to be the sounder advice: dropping the least significant variable or dropping the variable with the highest VIF? Or is there another option worth considering?




The major effect of ‘near multicollinearity’ is on the standard errors of the estimated coefficients. Take some time to focus on how these numbers are calculated. The estimated error variance (designated by in  Wooldridge) is the ratio of the residual sum of squares divided by <em>n</em> – <em>k</em> – 1; line 37 asks R to compute the estimated error variance, which equals <u>_______</u>.




Line 38 asks R to compute the square root of the previous term. The “Residual standard error” (designated by in  Wooldridge) is the square root of the estimated error variance. Write down the result shown in the regression table (Residual standard error = <u>_____</u>), and check that you get the same result when you run line 38 and the following line of code:

&gt; summary(final)$sigma

Run lines 40-41 to generate the <strong><em>variance-covariance matrix</em> <em>of the estimators</em></strong>. (I put this in <strong><em>bold and italic</em></strong> print, because we will be using this matrix more and more over coming weeks.)

&gt; vce &lt;- vcov(final)

The diagonal elements of this matrix are the variances of the coefficient estimates. If you take the square root of any diagonal element, you compute the standard error for the estimated coefficient!




Try it: run line 42 to take the square root of the second diagonal element, which is avginc:

&gt; sqrt(vce[2,2)

The result equals ______; the standard error for the coefficient for avginc shown by line 34 equals ______.




Line 44 provides a summary of the residual from the ‘final’ regression. Obviously the mean residual should equal 0, but when you type line 45, R also tells you the standard deviation of the residual (which equals _____ )… which is slightly <em>smaller</em> than the Residual standard error (which equaled <u>_____</u> ); do you know why? If not, ponder the equations until you figure this out.




Line 46 asks R for a histogram of residuals.




<ol>

 <li><strong><em> Model Fit</em></strong></li>

</ol>




Let’s review how the <em>R</em><sup>2</sup> statistic is calculated. Run lines 48-51 in the R script:

# Model Fit

final.res&lt;-resid(final)

resf&lt;-final.res^2

ssr&lt;-sum(resf); ssr




In your own words, describe what the residual sum of squares is, and then describe what steps are being taken when you these three lines of code. Please write down the value of the residual sum of squares (SSR = ______ ).




Next you can, obtain the total sum of squares by running lines 53-56:

summary(cadta$testscr); ybar &lt;- mean(cadta$testscr)

devy &lt;-(cadta$testscr-ybar)

devysq&lt;-devy^2

sst&lt;-sum(devysq); sst

Please write down the number that results (SST = ______ ) and describe in your own words what steps were taken to arrive at that number.




Now that you have the residual sum of squares (named <em>ssr</em>) and the total sum of squares (named <em>sst</em>), fill in for yourself one line of R code could you use to find the R<sup>2</sup>.

&gt;




<ol>

 <li><strong><em> Multicollinearity Redux</em></strong></li>

</ol>




Let’s keep our focus on the final regression (from line 34) with three explanatory variables (avginc, el_pct, and meal_pct), but now with a smaller sample. The reason for doing this is that multicollinearity is sometimes referred to as “micronumerosity,” because it results from a problem with the sample – too little “free” variation in one or more explanatory variables – that can be addressed by expanding the sample. In section 3.4, Wooldridge contends that multicollinearity and small samples are related problems, as you will soon observe.




Run line 61 to subset the data, selecting just the school districts in Los Angeles County, Orange County, and Ventura County; combined these three counties have 47 districts, compared to 420 in the entire state. (You can run lines 59-60  to see how many districts are in each county.)




Run line 63 to estimate the final model but with the smaller sample. Earlier you loaded the <em>stargazer</em> package; use that package now by running line 64, which will create a table of regression results allowing you to more easily compare models using the same specifications but different samples.




Compared to the same model that used the full sample, (a) what has happened to the model fit? (b) what has happened to the estimated coefficients? (c) what has happened to the standard errors of the coefficients?




Line 65 brings back the diagnostics you used earlier to assess multicollinearity. Are there any VIFs that we should be concerned about? Compare this output to line 34’s output.




Run line 66 to examine our small sample’s correlation matrix; compare this to line 28’s output. How did the correlation between el_pct and the other two explanatory variables (avginc and meal_pct) change from the large sample of 420 school districts to the smaller sample of 47 school districts?




Finally, run line 67 to examine our small sample’s scatterplots. If you compare this to line 10’s output, you should observe that the scatterplots involving el_pct and the other two explanatory variables look more line-like than cloud-like in the smaller dataset.