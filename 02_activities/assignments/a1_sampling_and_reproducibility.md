# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YOUR NAME

```
Please write your explanation here...

The whitby_covid_tracing.py file contains a simulation model that evaluates how contact tracing might bias the perceived sources of COVID-19 infections. Here's an analysis of the sampling procedures within the model:

Identify Sampling Stages in the Model
The whitby_covid_tracing.py simulation code involves a few stages of sampling:

1. Initial Population Sampling:
Function: simulate_event(m)
Procedure: A DataFrame ppl (with event, infected, and traced columns) is created with 1,000 individuals, where 200 attend weddings and 800 attend brunches.
Sample Size: 1,000 individuals
Sampling Frame: Attendees of weddings and brunches

2. Infection Sampling:
Function: simulate_event(m)
Procedure: A random subset of the population is infected based on the ATTACK_RATE (10%). This uses the np.random.choice function to select infected individuals.
Sample Size: 10% of 1,000 individuals (100 individuals)
Underlying Distribution:  Binomial distribution over the entire population, because each individual has a 10% independent chance of infection.

3. Primary Contact Tracing:
Function: simulate_event(m)
Procedure: Among the infected individuals, a random selection is traced based on the TRACE_SUCCESS rate (20%). This uses the np.random.rand function to decide if an infected person is traced.
Sample Size: 20% of infected individuals (approximately 20 individuals)
Underlying Distribution: Binomial distribution, because each infected individual has a 20% chance of being traced.

4. Secondary Contact Tracing:
Function: simulate_event(m)
Procedure: If the number of traced individuals at a specific event type exceeds the SECONDARY_TRACE_THRESHOLD (2), all infected attendees of that event are considered traced.
Sample Size: Variable, dependent on the number of traced individuals per event type exceeding the threshold.
Underlying Distribution: Conditional on the primary tracing results. It doesn’t strictly follow a standard probability distribution but rather a conditional sampling rule that depends on the outcome of prior events.

Relation to the Blog Post
The blog post discusses how contact tracing might overrepresent certain events (e.g., weddings) due to easier traceability compared to other settings (e.g., private gatherings). 
The sampling process in whitby_covid_tracing.py closely mirrors the real-world contact tracing challenges described in the blog. Primary and secondary tracing processes highlight how certain events become overrepresented due to easier tracing, leading to biased samples that can mislead policymakers or analysts about actual transmission patterns.
This simulation emphasizes the issue of non-random missing data in contact tracing and the risks of systematic bias when interpreting outbreak data—just as the blog warns that sampling is biased toward cases that are easier to trace.

Summary
The sampling procedures in the code are designed to simulate the potential biases introduced by contact tracing:
Initial Population Sampling: Sets up a structured population of event attendees.
Infection Sampling: Randomly infects a proportion of individuals.
Primary Tracing Sampling: Randomly traces a proportion of infected individuals.
Secondary Tracing Sampling: Applies additional tracing based on event-specific thresholds.
These steps collectively simulate how certain events might appear as more significant sources of infection due to the mechanics of contact tracing, aligning with the points raised in the blog post.


Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?
My answer:
The code only partially reproduced the graph from the blog post but with noticeable differences in distribution and layout; the code outputted graph did not capture the key bias effect emphasized in the original blog.
In the graph from the original blog post, "True proportion" is tightly clustered around 0.2, with the "Observed proportion" spread more widely between 0.2 and 0.6. This pattern suggests a significant bias in observed proportions due to contact tracing.
In contrast, the code outputted graph showed the majority of cases centered around lower proportions (around 0.15–0.25), with little spread compared to the graph from the blog post; the observed proportion distribution closely resembled the true proportion distribution and showed only a minor bias, with the observed and true proportions appearing quite similar.
The above mentioned difference could suggest that the simulation parameters or random factors in our code differ from those in the original post. 


Comment on the reproducibility of the results after modifying the number of repetitions in the simulation to 1000:
Across multiple runs with 1,000 repetitions, the overall shape and range of the outputted histograms remain consistent. The peaks, or modes, for each distribution (Traced to Weddings and Infections from Weddiongs) are centered around similar proportions (between 0.15 and 0.25), indicating a consistent central tendency.
Variation in Distributions:
Despite the consistent trend, there are noticeable variations in the specific shapes and peaks of the histograms. This is due to the reduced number of repetitions (1,000 compared to 50,000 in the original simulation), which increases the variability in the sampled outcomes.

Implications of Reduced Sample Size:
With fewer repetitions, the results are more sensitive to random fluctuations. Without a fixed random seed, some variability is expected when using a smaller repetition number like 1,000 simulations. Increasing the number of repetitions would reduce this variability, leading to more stable and reproducible results.

Changes Made to the Code for Reproducibility:
Global Random Seed: np.random.seed(10) is set at the beginning of the script to ensure that all random processes (like event infection and tracing) produce the same results each time the script is executed.

Parameterized Repetitions: The number of repetitions (num_repetitions) is passed to the run_simulation_and_plot function, ensuring that the number of simulations conducted can be easily adjusted without modifying the simulation logic itself.

These changes ensure that when we run the script multiple times, we will get identical simulation results, which is essential for reproducibility in scientific simulations and experiments.


```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
