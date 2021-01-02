# awesome-simple-QA

## datasets

### WebQuestions

https://github.com/brmson/dataset-factoid-webquestions or
https://nlp.stanford.edu/software/sempre/

It consists of 5,810 human-annotated questions, matched with answers corresponding to entities of Freebase. (no triple has to be returned, only a single entity). It was first used by Bordes et al. (2014b).

### SimpleQuestions

https://git.uwaterloo.ca/jimmylin/BuboQA-data/raw/master/SimpleQuestions_v2.tgz or
https://research.fb.com/downloads/babi/

The SimpleQuestions dataset consists of a total of 108,442 questions written in natural language by human English-speaking annotators each paired with a corresponding fact, formatted as (subject, relationship, object), that provides the answer but also a complete explanation. Facts have been extracted from the Knowledge Base Freebase. The authors randomly shuffle these questions and use 70% of them (75910) as training set, 10% as validation set (10845), and the remaining 20% as test set.

The annotators were explicitly instructed to phrase the question differently as much as possible.

#### FB2M and FB5M subsets

`/SimpleQuestions_v2/freebase-subsets/`

FB2M contains about 2M entities and 5k relationships. FB5M, is much larger with about 5M entities and more than 7.5k relationships. They were first used by Bordes et al. (2014a).

### 30M-Factoid

https://academictorrents.com/details/973fb709bdb9db6066213bbc5529482a190098ce

## baselines

### Bordes et al. (2014b), WSE (weakly supervised embedding models)

> Antoine Bordes, Jason Weston, and Nicolas Usunier. "Open question answering with weakly supervised embedding models." ECML-PKDD, 2014.


- [PDF](https://link.springer.com/content/pdf/10.1007/978-3-662-44848-9_11.pdf)
- CODE
- METHODOLOGY: `Both the question and the KB triple are embedded as a $k$-dimensional vector and compared based on inner product. In particular, each question token and each KB entity/predicate is learned as $k$-dimensional and the embeddings of questions and KB triples are summed based on their presences.`
- REMARKS:
  - questions can be regarded as a bag of words.
  - large question-answer datasets are generated by templates and their paraphrase to more types of questions are preserved by a multitask learning process over PARALEX dataset.

### Bordes et al. (2014a), SGE (subgraph embeddings)

> Antoine Bordes, Sumit Chopra, and Jason Weston. "Question answering with subgraph embeddings." arXiv preprint arXiv:1406.3676 (2014).

- [PDF](https://arxiv.org/pdf/1406.3676)
- CODE
- METHODOLOGY: `It extends the question token and KB entity/predicate embedding in Bordes et al. (2014a). However, it further embeds answer as path plus all connected entities to the answer (i.e., a subgraph), so as to answer more sophisticated questions that answers may not be directly connected to the question entities.`
- REMARKS:
  - how subgraph embedding is constructed: 1) each single entity is embedded, 2) the 1- and 2-hops paths are embedded, consisting of embeddings of start and end entities, and embeddings of relations in between; 3) the entire subgraph of entities connected to the candidate answer entity are all embedded, each is being represented as a entity embedding plus a relation type embedding.
  - its hypothesis is that including more information about the answer in itsrepresentation will lead to improved result.

### Bordes et al. (2015), MemNN (memory networks)

> Antoine Bordes, Nicolas Usunier, Sumit Chopra, and Jason Weston. "Large-scale simple question answering with memory networks." arXiv preprint arXiv:1506.02075 (2015).


- [PDF](https://arxiv.org/pdf/1506.02075)
- [CODE for MemNN](https://github.com/facebook/MemNN)
- METHODOLOGY: `It studies the simple question answering in a large-scale KG setting. First, it finds candidate facts by matching $n$-grams of words of questions to aliases of freebase entities and keeping all facts having one of the matching entities. Second, the scoring is performed using embedding model learned from memory networks that stores historical facts for supervision.`

### Golub and He (2016), CQAA (Character-level question answering with attention)


> David Golub, and Xiaodong He. "Character-level question answering with attention." EMNLP 2016.


- [PDF](https://arxiv.org/pdf/1604.00727)
- [CODE](https://github.com/davidgolub/SimpleQA)
- METHODOLOGY: `Questions are embedded as one-hot encodings of characters in the question based on LSTM encoder. each KG entity/predicate is embedded as a single embedding based on a character-level CNN-based enconder. An LSTM-based decoder with attention is integrated with a relevant function to find 1) head entity and 2) predicate to find candidate facts in KG. The probabilities of candidates are calculated based on cosine similarity between question and candidates. Candidate entities and predicates are selected as similar to Bordes et al. (2015), i.e., by substring matching.`

### Dai et al. (2016), CFO (Conditional focused)

> Zihang Dai, Lei Li, and Wei Xu. "CFO: Conditional focused neural question answering with large-scale knowledge bases." ACL 2016.

- [PDF](https://arxiv.org/pdf/1606.01994)
- [CODE](https://github.com/zihangdai/cfo)
- METHODOLOGY: `.`

### Yin et al. (2016), Simple question answering by attentive convolutional neural network

> Wenpeng Yin, Mo Yu, Bing Xiang, Bowen Zhou, and Hinrich Schütze. "Simple question answering by attentive convolutional neural network." COLING 2016.

- [PDF](https://arxiv.org/pdf/1606.03391)
- [CODE1](https://github.com/yinwenpeng/KBQA_IBM)
- [CODE2](https://github.com/yinwenpeng/KBQA_IBM_New)
- METHODOLOGY

### Lukovnikov et al. (2017), Neural network-based question answering over knowledge graphs on word and character level

> Denis Lukovnikov, Asja Fischer, and Jens Lehmann. "Neural network-based question answering over knowledge graphs on word and character level." WWW 2017.

- [PDF](https://dl.acm.org/doi/pdf/10.1145/3038912.3052675?casa_token=iLERoPpVmdgAAAAA:X0Wha2ssSGvCh2zWbm1glDTeBtzA9GlZXB7BcKsG7ZZEPj0Fvm18_zYyLoI1v5GGGSNU6uBN8SNg)
- [CODE](https://github.com/WDAqua/teafacto)
- METHODOLOGY

### Mohammed et al. (2018), Strong baselines for simple question answering over knowledge graphs with and without neural networks

> Salman Mohammed, Peng Shi, and Jimmy Lin. "Strong baselines for simple question answering over knowledge graphs with and without neural networks." NAACL 2018.

- [PDF](https://arxiv.org/pdf/1712.01969)
- [CODE](https://github.com/castorini/BuboQA)
- METHODOLOGY: `It consists of entity detection, entity linking, relation prediction, and evidence combination. In particular, the entity detection is first performed to identify the entity being queried through bi-LSTM. Subsequently, identified entity name is linking to KG entities by $n$-gram fuzzy matching. Then, relation is found through bi-GRU as a classification task over all possible relations. At last, all possible entity-relation pairs are evaluated based on the product of their component scores.`
- REMARKS:
  - several different baselines are proposed, and BiLSTM-BiGRU achieves the best results over simpleQuestions dataset.
  - it can actually be regarded as a non-embedding based method, however, it handles the simple QA problem in an information retrieval paradigm, as others.

### Hao et al. (2018), Pattern-revising enhanced simple question answering over knowledge bases

> Yanchao Hao, Hao Liu, Shizhu He, Kang Liu, and Jun Zhao. "Pattern-revising enhanced simple question answering over knowledge bases." COLING 2018.

- [PDF](https://www.aclweb.org/anthology/C18-1277.pdf)
- CODE
- METHODOLOGY: `It conducts pattern extraction and entity linking first to extract possible entity metion and question pattern, so as to reduce the candidates resulted from an $n$-gram matching. Then, pattern-revising over all candidate patterns are performed to correct the wrong pattern and get the right head entity mention. Then, a join fact search is performed that integrates the consine similaries between the LSTM encodings of entity and question as well as those of entity+relation and question. The LSTM encodings are generated in both character and word levels.`

### Gupta et al. (2018), Retrieve and re-rank: A simple and effective IR approach to simple question answering over knowledge graphs

> Vishal Gupta, Manoj Chinnakotla, and Manish Shrivastava. "Retrieve and re-rank: A simple and effective IR approach to simple question answering over knowledge graphs." EMNLP-FEVER 2018.

- [PDF](https://www.aclweb.org/anthology/W18-5504.pdf)
- CODE
- METHODOLOGY

### Petrochuk et al. (2018), Simplequestions nearly solved: A new upperbound and baseline approach

> Michael Petrochuk, and Luke Zettlemoyer. "Simplequestions nearly solved: A new upperbound and baseline approach." EMNLP 2018.

- [PDF](https://arxiv.org/pdf/1804.08798)
- [CODE](https://github.com/PetrochukM/Simple-QA-EMNLP-2018)
- METHODOLOGY: `The top-$k$ head entity recognition is performed first such that distribution of head entities over questions are modeled by a biLSTM and a linear-chain CRF. Then, the relation classfication is conducted over the given question and the candidate head entity by a bi-LSTM.`
- REMARKS:
  - For entity candidate selection, all hyperparameters are hand tuned and then alimited set are further tuned with grid search to increase validation accuracy. GLoVe embeddings and Adam were used for bi-LSTM model, and CRF is used to decode the K candidates with viterbi algorithm.
  - For relation classification, all hyperparameters of LSTM are hand tuned and then alimited set are further tuned with Hyperban.

### Huang et al. (2019), Knowledge graph embedding based question answering

> Xiao Huang, Jingyuan Zhang, Dingcheng Li, and Ping Li. "Knowledge graph embedding based question answering." WSDM 2019.

- [PDF](https://dl.acm.org/doi/pdf/10.1145/3289600.3290956?casa_token=_jdAPjXRy5MAAAAA:zjFI6xu8CC6rpBIRREu3aQCfpIxE4fmWVQ1Ru0mwzcuav2tjiRJyLLn91p0zjZ_THpXQB7sxMW8A)
- [CODE](https://github.com/xhuang31/KEQA_WSDM19)
- METHODOLOGY: `All KG entities and predicates are embeddings with TransE or TransR. Next, bi-LSTM with attention is applied to generate the corresponding KG embeddings of mentioned entity and predicate. Also, position of head entity mention is identified by a bi-LSTM and used to find candidates based on fuzzy matching. A joint similarity function is designed to integrate the similaries between entity/predicate embeddings and matched texts.`

### Zhao et al. (2019), Simple question answering with subgraph ranking and joint-scoring

> Wenbo Zhao, Tagyoung Chung, Anuj Goyal,andAngeliki Metallinou. "Simple question answering with subgraph ranking and joint-scoring." NAACL 2019.

- [PDF](https://arxiv.org/pdf/1904.04049)
- CODE
- METHODOLOGY

### Lukovnikov et al. (2019), Pretrained transformers for simple question answering over knowledge graphs

> Denis Lukovnikov, Asja Fischer, and Jens Lehmann. "Pretrained transformers for simple question answering over knowledge graphs." ISWC 2019.

- [PDF](https://arxiv.org/pdf/2001.11985)
- CODE
- METHODOLOGY

### Sharath et al. (2020), Question answering over knowledge base using language model embeddings

> Japa Sai Sharath, and Rekabdar Banafsheh. "Question answering over knowledge base using language model embeddings." IJCNN 2020.

- [PDF](https://arxiv.org/pdf/2010.08883)
- CODE
- METHODOLOGY

## Other Resources

### Relevant Papers

### GitHub Repository

- https://github.com/PetrochukM/Simple-QA-EMNLP-2018/
- https://github.com/simba0626/Question-Answering
- https://github.com/BshoterJ/awesome-kgqa
- https://github.com/simba0626/Question-Answering
