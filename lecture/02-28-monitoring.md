Announcements:

- Released comments on the project proposals, please share with other group members.


Note: come back to question: where to make it parallel?

```{r}

boot = function(recipient, n = 100){
    res = lapply(seq(n), function(...) NULL)
    NULL
}

bootparallel = function(recipient, n = 100){
    res = parallel::mclapply(seq(n), function(...) NULL)
    NULL
}


recipients = 1:1000

# Faster, 0.08 seconds
system.time(parallel::mclapply(recipients, boot))

# Slower, 6.574 seconds
system.time(lapply(recipients, bootparallel))

```


## Questions

For question 1 on homework, describe computation, shoot for less than half a page.
An itemized list would be good.
For example:
1. on the cluster, submit an sbatch to select columns you need.

Summarize the distribution of KLD:
mean, median, quantiles, plot histogram,

```{r}
d = 1:9
q = log10(1 + 1/d)

# From the counts
actual = q + 0.01 * rnorm(9)

uniform = rep(1 / 9, 9)

plot(d, q, type = "l")
lines(d, actual, lty = 2)

lines(d, uniform, lty = 3)

```

## Review

Yesterday we mostly talked about how data should flow and be transformed for this assignment.
Data flow is the concept behind software such as tensorflow and Apache Pig.

The contingency table contains counts of all the digits by recipient is all that you need to complete the rest of the assignment.
You can calculate it and then save it in your home directory or download it to your local laptop.


## Cluster Usage

We are 60 people simultaneously using shared compute resources.
Yesterday several students lost 25% of their points on HW4 for not cleaning up `/scratch`.

It's not that leaving files on `/scratch` is such a terrible sin.
It's that I told the class several times in lecture and on Piazza to clean it up, yet it didn't happen.
These students didn't know they left the files there.

These are the rules that will ensure that everyone has a full opportunity to use the cluster and complete the assignment.

If you're not sure whether you're breaking a rule, then check and ask.


### Files:

- OK: Leave files in your home directory
- NOT OK: Leave files in any shared directories, including `/scratch` 

Let me know if you are going to use a shared file for the project- that's no problem.

We'll check for stray files after the assignment date closes.


### Resource Usage:

On our `staclass` partition:
- Only use 2 cpus i.e. with `--cpus-per-task=2` argument to `srun` or `sbatch` or by running two different jobs
- Cancel jobs if they take longer than 24 hours (`scancel`)
- Cancel jobs that use an excessive amount of memory- more than 50%

I don't care as much what you do while you're NOT on the `staclass` partition, since that won't affect the rest of the students.
Go ahead and use up to a full node to do the bootstrap in parallel- that's 32 cores and 64 GB memory.

This weekend we'll check for jobs that are in violation, and cancel them if we need to.


## Projects

Please share feedback with your team.

Project notes:
Feel free to use the [usaspending web browser](https://www.usaspending.gov/#/explorer) to get started, but your projects should go beyond that.
Here are some common things that I noted:

- Adjust for inflation
- Handle duplicates
- Specific questions are easier to answer.
    It can take time to narrow them down.
    Many of the proposals are vague.
- Listing external data sources


## Streaming in R

See `examples/first_char_last_col.R`


## Profiling


