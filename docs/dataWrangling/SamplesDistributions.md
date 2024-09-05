# Populations, Samples, and Distributions

As we muddle through MATLAB and data analysis, we will also be muddling through some basic concepts in statistics. Here are some concepts and terminology you should know.

## Populations and Samples

- **Population (N)**: the complete set of items or events that share a common attribute, from which data can be gathered and analyzed. Whatever it is that you want to know about.
- **Sample (n)**: a subset of the Population
  - **Non-probablity Sampling:** A sample from what's available, what was convenient to collect
  - **Random Sampling:** Samples selected based on randomized technique designed on increase the validity (or representativeness) of the sample

![img-name](images/US-PopvSample.png){ width="550"}

>**Examples of Populations vs samples.** Populations (in pink) can be All US Citizens, all Adult US citizens, or even just adult citizens in the state of Colorado. Samples (in yellow) would be subsets of whatever you define as your population.

## External Validity

The key to a good sample is that it is representative of the entire population. For example, if your population is 50% women, than your sample should be 50% women.

External Validity is a just a fancy term for defining how representation your sample is of the population.

- **High external validity**: Your sample is representative
- **Low external validity:** not so much. Your sample may have some bias or is too small (and maybe has a large number of outliers)

![img-name](images/Sample-inference.png){ width="350"}

>With a representative sample that has high external validity, you can make inferences (or predictions) about the population at large.

## Distributions

A Normal distribution, also known as the Gaussian distribution, is a probability distribution that appears as a "bell curve" when graphed. The normal distribution describes a symmetrical plot of data around its mean value, where the width of the curve is defined by the standard deviation.

### Empirical Data

For all normal distributions, 68.2% of the observations will appear within plus or minus one standard deviation of the mean; 95.4% will fall within +/- two standard deviations; and 99.7% within +/- three standard deviations.

This fact is sometimes called the "empirical rule," a heuristic that describes where most of the data in a normal distribution will appear. Data falling outside three standard deviations ("3-sigma") would signify rare occurrences.


![img-name](images/normal-distribution-1024x640.webp){ width="650"}

## Useful Resources

- [Investopedia Analysis Tools](https://www.investopedia.com/tools-for-fundamental-analysis-4689755)
  - [Populations](https://www.investopedia.com/terms/p/population.asp)
  - [Normal Distribution](https://www.investopedia.com/terms/n/normaldistribution.asp#:~:text=The%20Bottom%20Line-,Normal%20distribution%2C%20also%20known%20as%20the%20Gaussian%20distribution%2C%20is%20a,defined%20by%20the%20standard%20deviation.)
- [Psych Explained YouTube series](https://www.youtube.com/@PsychExplained)
  - [Random Sampling](https://www.youtube.com/watch?v=r-rFO_2NsgI&list=PL_pCzdGjrXUXiNIaoUNjjxZ4sAu8ypV-y&index=6)
  - 