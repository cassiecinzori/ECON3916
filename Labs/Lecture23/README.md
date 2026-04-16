# FedSpeak Analysis - NLP on FOMC Minutes

**Objective:** Applied natural language processing to two decades of Federal Reserve meeting minutes to quantify shifts in monetary policy sentiment and identify distinct communication regimes across major economic cycles.

## Methodology

- Loaded FOMC meeting minutes via HuggingFace `gtfintechlab/FOMC_Minutes` and parsed meeting dates across the full available time series
- Preprocessed raw text through a standard NLP pipeline: lowercasing, non-alphabetic character removal, tokenization, stop word filtering, and WordNet lemmatization
- Built a TF-IDF document-term matrix with unigrams and bigrams (`min_df=5`, `max_df=0.85`, `max_features=3000`) to capture policy-relevant vocabulary while filtering noise and background filler terms
- Computed Loughran-McDonald sentiment scores - net sentiment ((positive - negative) / total words) and uncertainty score (uncertainty words / total words) - using a domain-specific financial lexicon calibrated for institutional text
- Visualized rolling sentiment and uncertainty time series with annotations at key macro events: Lehman Brothers collapse, taper tantrum, COVID shock, and the 2022 tightening cycle
- Applied TruncatedSVD (50 components) to the sparse TF-IDF matrix before fitting K-Means (K=3) to identify latent language regimes in Fed communication
- Compared pre-COVID and post-COVID sentiment distributions via overlaid KDE plots to quantify structural shifts in Fed language following March 2020

## Key Findings

K-Means clustering on the TF-IDF vectors recovered three historically coherent language regimes roughly corresponding to the pre-crisis conventional policy era, the post-2008 unconventional policy period (zero lower bound, QE, forward guidance vocabulary), and the post-COVID tightening cycle - suggesting that major policy pivots leave detectable signatures in the text itself, not just in rate decisions. Sentiment analysis confirmed that post-COVID minutes are both more negative and more uncertain on average than the pre-2020 baseline: the 2020 shock introduced a wave of crisis language, and the 2022-2023 tightening cycle sustained elevated negative sentiment through persistent references to inflation, supply constraints, and geopolitical risk. The uncertainty score divergence between periods reflects the Fed's shift from the stable, data-dependent forward guidance of the 2010s to more hedged, conditional language appropriate for a novel macro environment with no clear historical precedent.
