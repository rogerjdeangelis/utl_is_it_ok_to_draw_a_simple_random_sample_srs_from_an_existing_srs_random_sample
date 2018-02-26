# utl_is_it_ok_to_draw_a_simple_random_sample_srs_from_an_existing_srs_random_sample
Is it ok to draw a simple random sample(SRS) from an existing  SRS random sample.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Is it ok to draw a simple random sample(SRS) from an existing  SRS random sample

    I have a 250,000  SRS from some 240 million observations, but I need 100,000. Can I draw 100,000 from the
    existing 250,000 SRS. The input is for a trajectory analysis(like time series cluster analysis).
    
    github
    https://goo.gl/v1nrf4
    https://github.com/rogerjdeangelis/utl_is_it_ok_to_draw_a_simple_random_sample_srs_from_an_existing_srs_random_sample

    Bottom line for me

       It is ok but...

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


