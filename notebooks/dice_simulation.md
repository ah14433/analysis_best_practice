---
title: "Dice simulation"
output:
  html_document:
    df_print: paged
---

With this [R Markdown](http://rmarkdown.rstudio.com) Notebook, we can make a simulated version of the experiment we just did that is much easier to reproduce.

When you execute code within the notebook, the results appear beneath the code. Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd+Shift+Enter*. 


```r
# This code snippet generates a random number between 1 and 20 (inclusive), simulating rolling the dice once.
dice_roll <- sample(1:20,1)
dice_roll
```

```
## [1] 9
```

If you run this code snipped you'll probably get a different number than me (and if you keep running the code you will continue to get new random numbers) since the numbers are randomly generated. 
In the interests of reproducibility, it is sometimes useful to have the same "random" numbers by setting the seed.


```r
set.seed(12345)
dice_roll <- sample(1:20,1)
dice_roll
```

```
## [1] 15
```

Running the above chunk of code will always give the same number (15) assuming that the seed is unchanged.


```r
# Dice experiment 1 - How often is a null finding found to be significant?
repeats = 1000
false_positives = 0
num_rolls = 1
for (i in 1:repeats){
  dice_roll = sample(1:20,num_rolls)
  if (dice_roll==1){
    false_positives = false_positives+1
  }
}
print(false_positives/repeats)
```

```
## [1] 0.047
```
As we'd expect, experiment 1 shows us that there's roughly a 1 in 20 (0.05) of getting false positives using a 0.05 significance rate.



```r
# Dice experiment 2 - How often will we get a "significant result" if we check 20 different things?

repeats = 1000
num_rolls = 20
false_positives = 0
for (i in 1:repeats){
  simulated_data = sample(1:20,num_rolls,replace=TRUE) # replace=TRUE allows repeated numbers.
  if(sum(simulated_data==1)>0){
    false_positives=false_positives+1
  }
}
print(false_positives/repeats)
```

```
## [1] 0.636
```
Experiment 2 shows the effect of p-hacking. With a 1 in 20 chance of having any individual experiment have a false positive, but trying 20 different hypotheses, we have a better than 50% chance of getting a false positive. 
