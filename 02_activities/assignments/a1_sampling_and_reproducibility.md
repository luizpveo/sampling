# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YOUR NAME

```
Please write your explanation here...

Question 1:  
Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Stage 1 - Infect a random subset of people: 
Procedure: Selects a group of individuals to be infected (based on the ATTACK_RATE = 0.10).
Function used: np.random.choice
Sample Size: Determined by int(len(ppl) * ATTACK_RATE), which calculates the number of people to infect based on the attack rate. (10% of the total population) 
Sampling Frame: The entire population attending events (ppl.index), which includes both wedding and brunch attendees.

Stage 2 - Primary Tracing Sampling:
Function used: np.random.rand in combination with a comparison operation (< TRACE_SUCCESS).
Sample Size: The number of infected person (sum(ppl['infected']))
Sampling Frame: Infected individuals.

Stage 3 - Secondary Tracing Determination: 
Procedure: This step is conditional on the counts of traced individuals at each event.
Function Used: ppl.loc[ppl['event'].isin(events_traced) & ppl['infected'], 'traced'] = True
Sample Size: It’s dependent on the number of events meeting the secondary trace threshold.
Sampling Frame: : Events with traced cases.

Question 2:
Does this code appear to reproduce the graphs from the original blog post?
No, the graph looks different from the original blog post.

Question 3:
Comment on the reproducibility of the results.
Without a seed or similar setting, the output graphs will vary each time the script is run due to the lack of reproducibility.

Question 4:
Describe the changes you made to the code and how they affected the reproducibility of the script file.
I added the Random State Object as a parameter in the simulate_event function to control randomness and created a np.random.RandomState object with the seed 10 to ensure all random operations use the same seed.
These adjustments ensure that the results are consistent across different runs of the script, enhancing reproducibility.


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
