# The gene-level DNA methylation-based aging clock

## 1.DNA methylation age prediction model

We built a gene-level DNA methylation-based (beta value) regression model for DNA methylation age prediction. 

### Example: METABRIC cohort prediction

Our study used the METABRIC datasets. Here, we show how to obtain DNA methylation age using our model.

```r
load("aging_clock.rda")
load("METABRIC_example.rda")

# Check features used in our model
gene.feature <- rownames(DNAm.aging.clock$fit$beta)
table(gene.feature %in% rownames(metabric.expr.df))

# prepare data.frame
# metabric.expr.df is a gene-level methylation beta value expression matrix.
pre.df = metabric.expr.df[gene.feature,]

# DNA methylation age prediction (transformed age)
pred.age <- predict(
  DNAm.aging.clock$fit, ## the model
  t(pre.df) ## DNA methylation matrix (gene in column)
)[,1]

# The predicted DNA methylation age in years
DNAm.aging.clock$inverse.F(pred.age)
```
