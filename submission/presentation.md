---
title: "Approaches to continuous risk-based benefit assessment"
subtitle: "A simulation study"
author: Alexandros Rekkas
header-includes:
  - \usepackage{amssymb}
  - \usepackage{amsmath}
  - \usepackage{bm}
  - \newcommand\given[1][]{\:#1\vert\:}
output:
  ioslides_presentation:
    smaller: TRUE
    keep_md: TRUE
    transition: default
    widescreen: TRUE
  beamer_presentation: default
---




<style type="text/css">
slides > slide:not(.nobackground):after {
  content: '';
}
</style>

<style>
div.footnotes {
  position: absolute;
  bottom: 0;
  margin-bottom: 10px;
  width: 80%;
  font-size: 0.6em;
}
</style>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<script>
  $(document).ready(function() {
    $('slide:not(.backdrop):not(.title-slide)').append('<div class=\"footnotes\">');

    $('footnote').each(function(index) {
      var text  = $(this).html();
      var fnNum = (index+1).toString().sup();
      $(this).html(text + fnNum);

      var footnote   = fnNum + ' ' + $(this).attr('content') + '<br/>';
      var oldContent = $(this).parents('slide').children('div.footnotes').html();
      var newContent = oldContent + footnote;
      $(this).parents('slide').children('div.footnotes').html(newContent);
    });
  });
</script>


## Subgroup analyses
* Generalizing overall treatment effects is often problematic
* Subgroup analyses rarely adequately powered




## Subgroup analyses
Subgroup analyses can be divided into 4 categories (***<footnote content="Varadhan R, Segal JB, Boyd CM, Wu AW, Weiss CO. A framework for the analysis of heterogeneity of treatment effect in patient-centered outcomes research. <em>Journal of clinical epidemiology</em>. 2013 Aug 1;66(8):818-25.">Varadhan et al, 2013</footnote>***):

* Confirmatory heterogeneity of treatment effect analysis	
* Exploratory heterogeneity of treatment effect analysis	
* Descriptive heterogeneity of treatment effect analysis	
* ***Predictive heterogeneity of treatment effect analysis***


## <footnote content="Rekkas, A., Paulus, J.K., Raman, G., Wong, J.B., Steyerberg, E.W., Rijnbeek, P.R., Kent, D.M. and van Klaveren, D., 2020. Predictive approaches to heterogeneous treatment effects: a scoping review. <em>BMC Medical Research Methodology, 20(1)</em>, pp.1-12.">Predictive HTE methods</footnote>
***Risk modeling***

 * A multivariate regression model $f$ that predicts the risk of an outcome $y$ based on the predictors $x_1\dots x_p$ is identified or developed.
 * The expected outcome of a patient receiving treatment $T$ (where $T = 1$, when patient is treated and $0$ otherwise) based on the linear predictor 
 $$lp(x_1,\dots x_p) = a + \beta_1x_1 +\dots\beta_px_p$$ 
 from a previously derived risk model can be described as
 $$E\{y|x_1,\dots,x_p\} = f(lp + \gamma_0T+\gamma T\times lp)$$

## Risk-based HTE
***<footnote content="Kent, D.M., Paulus, J.K., Van Klaveren, D., D'Agostino, R., Goodman, S., Hayward, R., Ioannidis, J.P., Patrick-Lake, B., Morton, S., Pencina, M. and Raman, G., 2020. The predictive approaches to treatment effect heterogeneity (PATH) statement. <em>Annals of internal medicine, 172(1)</em>, pp.35-45.">Reasoning </footnote>***

* When risk is described through a combination of factors the control event rate will typically vary considerably across the trial population. 
* The absolute risk difference will generally vary across risk strata even if the relative risk is the same 
* When a trial population has substantial variation in outcome risk, important differences often exist in harm–benefit tradeoffs

## Individualized approaches

* Stratification approach may not provide adequate prediction of benefit
* "Jumps" at cut-offs are not realistic
* Implement a risk-based smoothing approach

## Setting
For all patients we observe covariates $x_1,\dots,x_8$, of which $4$ are continuous and $4$ are binary. More specifically,

$$x_1,\dots,x_4 \sim N(0, 1)$$
$$x_5,\dots,x_8 \sim B(1, 0.2)$$

Generate the binary outcomes $y$ for the untreated patients ($t_x=0$), based on 

$$P(y\given x, t_x=0) = g(\beta_0 + \beta_1x_1+\dots+\beta_8x_8) = g(lp_0),$$

where $$g(x) = \frac{e^x}{1+e^x}$$

## Setting
For treated patients, outcomes are generated from:

$$P(y\given x, t_x=1) = g(lp_1)$$


where $$lp_1 = \gamma_2(lp_0-c)^2+\gamma_1(lp_0-c)+\gamma_0$$

## Setting
**Base-case scenario**

- Constant odds ratio: 0.8
- Sample size: 4250
- Outcome incidence, if left untreated: 20%
- Prediction model "true" AUC: 0.75

**Deviations(A)**

* Sample size: 1064, 17000
* Overall treatment effect: 0.5, 1
* Prediction performance: 0.65, 0.85

## Setting
<div class="figure">
<img src="/home/arekkas/Documents/Projects/epi_meeting_presentation/figures/deviate_linear_08.png" alt="Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)" width="50%" /><img src="/home/arekkas/Documents/Projects/epi_meeting_presentation/figures/deviate_quadratic_08.png" alt="Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)" width="50%" />
<p class="caption">Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)</p>
</div>

## Setting
<div class="figure">
<img src="/home/arekkas/Documents/Projects/epi_meeting_presentation/figures/deviate_linear_absolute_08.png" alt="Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)" width="50%" /><img src="/home/arekkas/Documents/Projects/epi_meeting_presentation/figures/deviate_quadratic_absolute_08.png" alt="Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)" width="50%" />
<p class="caption">Linear and quadratic deviations from the base-case scenario of constant relative effect (OR=0.8)</p>
</div>

## Setting
Finally, we consider 3 additional scenarios of interaction of individual covariates with treatment. These scenarios include a 4 weak interactions ($\text{OR}_{t_x=1} / \text{OR}_{t_x=0}=0.82$), 4 strong interactions ($\text{OR}_{t_x=1} / \text{OR}_{t_x=0}=0.61$), and 2 weak and 2 strong interactions.

## Methods
**Constant treatment effect**
$$E\{y\given x,t_x\} = P(y\given x, t_x) = g(\beta_0+\beta_1x_1+\dots+\beta_8x_8+\gamma t_x)$$
Absolute benefit is estimated from:
 $$\hat{f}_{\text{benefit}}(lp\given x, \hat{\beta}) = g(lp) - g(lp+\hat{\gamma}) $$

## Methods
**Linear interaction**
$$E\{y\given x, t_x, \hat{\beta}\} = g\big(lp+(\delta_0+\delta_1lp)t_x\big)$$

Predict absolute benfit from:
$$\hat{f}_{\text{benefit}}(lp\given x, \hat{\beta}) = g(lp) - g\big(\delta_0+(1+\delta_1)lp\big)$$

## Methods
**Non-linear interaction**
$$f_{\text{benefit}}(lp\given x,\hat{\beta}) = \hat{f}_{\text{smooth}}(lp\given x, \hat{\beta}, t_x=0) - \hat{f}_{\text{smooth}}(lp\given x, \hat{\beta}, t_x=1)$$
We consider three different approaches to smoothing:

- Loess
- Restricted cubic splines
- Local likelihood

## Evaluation

**Root mean squared error**

Assuming that $\tau(x)=E\{y\given x, t_x=0\} - E\{y\given x,t_x=1\}$ is the true benefit for each patient and $\hat{\tau}(x)$ is the estimated benefit from a method under study, the ideal loss function to use for the considered methods would be the unobservable root mean squared error $E\big\{(\hat{\tau} - \tau)^2\given x\big\}$.

We will estimate the RMSE from
$$\text{RMSE}=\frac{1}{n}\sum_{i=1}^n\big(\tau(x_i) - \hat{\tau}(x_i)\big)^2$$

## Evaluation
**C-for-benefit**

- Match patients on predicted benefit
- Use differences of observed outcomes within pairs as "observed benefit"
- Proceed with calculation of the concordance statistic

**Calibration for benefit**

- Match patients on predicted benefit
- Use differences of observed outcomes within pairs as "observed benefit"
- Fit smooth calibration curve
- Calculate the <footnote content="Austin, PC, Steyerberg, EW. The Integrated Calibration Index (ICI) and related metrics for quantifying the calibration of logistic regression models. <em>Statistics in Medicine<em>. 2019; 38: 4051– 4065.">integrated calibration index</footnote>
