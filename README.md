# utl_is_it_ok_to_draw_a_simple_random_sample_srs_from_an_existing_srs_random_sample
Is it ok to draw a simple random sample(SRS) from an existing  SRS random sample.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Is it ok to draw a simple random sample(SRS) from an existing  SRS random sample

    I have a 250,000  SRS from some 240 million observations, but I need 100,000. Can I draw 100,000 from the
    existing 250,000 SRS. The input is for a trajectory analysis(like time series cluster analysis).
    
    github
    https://goo.gl/v1nrf4
    https://github.com/rogerjdeangelis/utl_is_it_ok_to_draw_a_simple_random_sample_srs_from_an_existing_srs_random_sample

    Bottom line for me

       Looks like it is ok, But..

       If each random variable outcome in 250 has an equal chance then each of the 100,000 outcomes would also have an equal chance from target.
       Each random variable outcome is independent of all other random variable outcomes within a sample.      
       Statistics drawn from the two samples are not independent.
       But if I publish or do extensive inference I will draw the 100,000 from the full population to avoid explanation.
    
    Thanks in Advance

    Key Responses


    Peter Flom via listserv.uga.edu
    Feb 20 (6 days ago)
     to SAS-L
    There’s different degrees of purity in how “random sample” is defined.

    The strongest or purest is that every possible sample can be drawn and that you can assign
    likelihoods to each (usually equal likelihoods).
    If SAS’ random sampler follows this definition (and I believe it does, though I am not a specialist)
    then a random sample of a random sample is still OK, as far as I can see, because any possible
    sample could have been in the first sample and thus in the subsample.
    But I could be wrong. This stuff is notoriously unintuitive and, in my real work, we never have
    anything close to a real random sample anyway!

    Peter


    Martin, Vincent (STATCAN) via listserv.uga.edu
    Feb 23 (3 days ago)
     to SAS-L

    I haven’t dabbled in sample coordination theory much but IIRC the case of SRS from <the complement of>
    another SRS is the default case study in negative sample coordination, a method frequently used in
    large survey agencies albeit with more complex sample designs than SRS. The resulting sample is still an
    SRS per the definition that every possible sample of size n2 from the origina
    l population N has an equal probability to be sampled even from the 2-steps conditional process. The key
    difference is that the samples will not be independent, regardless that the second is drawn from
    the first or from the complement.

    Thus, provided you don’t make any inference comparing the 250k and 100k samples as if they were
    independent samples from your population, I believe your approach is fine with respect to sampling theory.
    Even though I don’t think John’s suggested brute force approach is what would be implemented in
    this situation, by definition, an SRS sample of n2=100k from the original population is achieved
    if all possible n2 sized samples had equal probability to be sampled. So whether there is (re)
    sorting or not at the second level does not affect that. Any given n2 sized sample from the orig
    inal population could have been assigned the n2 smallest random numbers at step 1 with equal probability.
    It most definitely changes the perceived randomness but not the sample selection probabilities with
    respect to the original population.

    I still would only take that approach in a dimensionality reduction context which is what I believe
    Roger is doing, if execution time of sampling from the original population was too costly
    for my purpose both for the peace of mind and so as to avoid having to carry the justification/demonstration
    if the results were to be presented to colleagues, clients, etc.

    *Negative Coordination defines coordinating samples across multiple surveys or multiple cycles from
    the same surveys that are drawn from the same frame (target population) in a manner so as to minimize
    overlap between samples. In its simplest form with 2 samples when n1+n2<N, sampling from the complement
    achieves that for SRS sampling. This is generally done to minimize response bu
    rden at the individual frame unit level so it is quite popular in household surveys and outside the
    take-all stratum for business surveys. In a survey context, Roger’s scenario would be positive
    coordination which is sometimes used for longitudinal studies or periodic surveys that require
    some stability in the estimates over time.
    As for the purpose of the task, I’d need more details to evaluate whether SRS is appropriate for it.

    Vincent Martin
    Methodologist – Social Survey Methods Division
    Statistics Canada / Government of Canada
    vincent.martin@canada.ca / Tel: 613-853-7135

    Méthodologiste – Division des méthodes d’enquêtes sociales
    Statistique Canada / Gouvernement du Canada
    vincent.martin@canada.ca / Tél: 613-853-7135

    Daniel Nordlund via listserv.uga.edu
    2:46 AM (6 hours ago)
     to SAS-L

    John,

    I guess I have to disagree.

    To obtain a simple random sample of size n from a POPULATION, the process must ensure that
      1. each member of the POPULATION has an equal probability of selection AND
      2. each possible sample of size n from the POPULATION has an equal probability of occurring

    When taking a simple random sample of size 100,000 from an existing sample of 250,000 from the
    given population, neither of the above conditions is satisfied. Most members of the population
    have zero probability of being selected, and most subsets of 100,000 (in the population) have
    zero probability of occurring.

    It was pointed out by John and Joe that if the the first 250,000 sample was not ordered, then
    one could just take the FIRST 100,000 as a random sample of the POPULATION.  And that is true,
    because each member of the POPULATION (1) had an equal chance of being selected in the first
    100,000 and (2) each potential sample of size 100,000 had an equal chance of being in that first 100,0
    00.  But again, taking any other sample of 100,000 from the 250,000 sample violates both of those principles

    This doesn't mean that a simple random sample of 100,000 isn't, in some sense, "representative"
    of the POPULATION.  For many purposes it may be quite adequate.  But, it is not a simple random sample of the POPULATION.

    Roger's original question: Is it ok to draw a random sample from a random sample?  I think the answer
    is "It depends."  I am reminded of the quote "In theory, there is no difference between theory and practice.
    But, in practice, there is."  (sorry I don't know the source) Drawing a simple random sample from a simple
    random sample of a population will lead to a biased sample, with r
    espect to the population.  The bias may be small/inconsequential but biased nonetheless.  Roger will need
    to decide whether that is a problem.
    
    
        Martin, Vincent (STATCAN) via listserv.uga.edu

    The formal definition of SRS is equal probability of all n-sized samples.
    The individual record-level inclusion probabilities is simply a consequence.
    However, the latter is not a sufficient condition for the former. Systematic
    sampling is the usual example of equal probability at the record level with
    unequal probability across all possible samples (assuming N/n is integer valued
    for simplicity and non-random initial sort).

    As for the argument provided, you are looking at the conditional sampling
    of the second step only with respect to the entire population but as John
    pointed out, you have to consider the entire process and when considered,
    all resulting n2=100k sized samples from the 2-steps meet the condition
    mentioned above.

    Let
    S1 be the space of all possible s1 samples of size n1 from N
    S2 be the space of all possible s2 samples of size n2 from s1
    S3 be the space of all possible s3 samples of size n2 from N

    All are subsets of the set of all possible samples of any size on a
    population of size N (omega in traditional set theory applied to sampling anyway).

    Using c() as the shorthand for the combinatorial or comb() function
    in SAS if you wish to write the formula down.

    The probability that any given sample s3 of size n2 is drawn through
    the 2-step process can be calculated by conditioning step 1 samples
    and then using bayes formula to further condition on whether s3 was
    fully contained within s1. So treating s3 as an arbitrary but fixed
    sample (i.e. randomness for probabilities below is WRT s1 and s2
    sampling mechanisms) and looking at the probab
    ility that this sample be drawn by the random 2-step process, you will find that

    -There are exactly c(N, n1) distinct samples of size n1 from step 1.
    So P(s1) = 1/comb(N, n1) forall s1 in S1.

    -There are exactly c(N-n2, n1-n2)*c(n2, n2) distinct samples of size n1
    that contain exactly s3. c(n2, n2) reduces to 1 it's just simple to see
    the combinatorial formula if you write it down. So the probability that
    the first step sample s1 contains an arbitrary s3 sample is
    P(s1 contains s3) = c(N-n2, n1-n2) / c(N, n1).

    -There are exactly c(n1, n2) distinct samples of size n2 from n1 at
    step 2 so P(s2 | s1) = 1/c(n1, n2) forall s2 in S2. There are exactly
    one such sample s3 if s3 is included in s1 and 0 otherwise such that
    P(s2 contains s3 | s1 contains s3) = 1/c(n1, n2) and P(s2 contains
    s3 | s1 does not contain s3)

    Thus, the probability that an arbitrary sample s3 be drawn from the
    joint 2 step process can be broken down by conditioning on step 1 and
    on whether s3 was nested in s1 or not. That is with s3 fixed, s1 and s2 random,

    P(s2 contains s3 , s1)

    =P( s2 contains s3, s1 contains s3) + P(s2 contains s3, s1 does not contain s3)
    =P(s2 contains s3 | s1 contains s3)*P(s1 contains s3)+
    P(s2 contains s3 | s1 does not contain s3)*P(s1 does not contain s3)
    = P(s2 contains s3 | s1 contains s3)*P(s1 contains s3)+0
    =[1/c(n1, n2)]*[ comb(N-n2, n1-n2) * [1/comb(N, n1)]]
    =[n2! (n2-n1)!/n1!]*[(N-n2)!/((n1-n2)!(N-n1)!)]*[n1!(N-n1)!/N!]
    =n2!(N-n2)!/N!
    =1/c(N, n2)

    Which is the exact probability of sampling any s3 from S3 via SRS.

    Tl;dr the 2 step process has exactly the same probability to draw any
    sample of size n2 from population N as an SRS sample of the same size
    drawn directly from the same population.

    It is naturally extremely difficult to make abstraction of conditional
    stuff. I have given up arguing with family members over probabilities
    when playing cards specifically because of that.


    Please forgive the very crude notation abuse, hopefully the abstraction
    of the problem is still readable. Set theory is awful to write in plain
    text and admittedly, I haven't done much formal set theory stuff in recent years.

    HTH,
    Vincent Martin


