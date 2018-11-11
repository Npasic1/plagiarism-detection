Plagiarism detection

Task: create system which accepts a set of input papers and detects plagiarism in that set.

Proposed solution:
- Split each paper into sentences and vectorize sentences using NLTK
- Use K-Means algorithm to cluster sentences from all the papers
- Initial centroids are set as vectorized sentences which are made up of most commonly used words from that paper (tried with 10,20,50 words, didn’t make much of a difference)
- The idea is that sentences that came from the same paper will end up in the same cluster - sentences from other papers which end up in this cluster would possibly be plagiarized
Results:
- When running the program on a sample of 50 papers, the results were inconclusive
- Each cluster had sentences from ~45 different papers (add screenshot) although there are dominant papers in each one which indicates that with appropriate adjustments this method might prove useful in plagiarism detection


Improvement ideas:
- Use a different model/method for sentence vectorization (currently using Spacy pretrained model)
- Is it possible for a centroid to have multiple points? Is it possible place multiple points in the clusters initially?
- Have a different strategy for choosing initial centroids (rather than simply looking at most common words, find most important sentences - maybe using TFIDF to determine them)
- Use another implementation of K-Means which allows us to set a distance function (sklearn K-Means uses Euclidean by default) - find distance functions which might be better for semantic clustering
- Use a different clustering algorithm - research algorithms used in market basket analysis (similarly to how we determine clusters of customers based on the items of their shopping cart, we could look at the papers as carts and their sentences as items we could detect strong relationships between sentences from different papers which would indicate plagiarism)
- rather than clustering sentences cluster trigrams (using KMeans or another algorithms)
- rather than clustering sentences cluster paragraphs of text - in most cases of plagiarism the plagiarised paper will have more than one plagiarised sentence (maybe use something like this to split paper into paragraphs https://www.nltk.org/api/nltk.tokenize.html#module-nltk.tokenize.texttiling)
- research different methods which compute text similarity which might not be based on clustering
- try a supervised learning approach with a labeled dataset (each paper would be labeled as plagiarised or not plagiarised). However, finding an appropriate dataset not just in terms of it being labeled but being broad enough to avoid overfitting the model to specific papers is challenging itself
- if none of these prove to be a viable solution, try intrinsic plagiarism detection which would detect chunks of text which differ from most of the text by style etc. At the moment, I assume this would not be a good approach in detecting plagiarism in academic papers because if part of the paper is plagiarized it is probably adjusted to fit the rest of the paper so we might not be able to detect plagiarism in this case with this method