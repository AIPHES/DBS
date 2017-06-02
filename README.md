# DBS – A summarization corpus of coherent extracts

The DBS corpus contains 93 multi-document summaries for 293 German documents about 30 education-related topics. We sampled the topics from the [Deutscher Bildungsserver](https://www.bildungsserver.de) (DBS) webpage and crawled the documents linked there. The documents are highly heterogeneous in terms of text type, genre, and style.

The multi-document summaries are the result of a seven step annotation process yielding *coherent extracts* – a novel type of summary that is based on phrases extracted from the original documents that have been ordered and minimally redacted to form a well-readable, coherent text. The data of all intermediate steps is part of the repository to allow for extensive system evaluation.    

If you use the corpus in academic works, please cite our COLING paper:

```
  @InProceedings{coling2016,
    author = {Benikova, Darina and Mieskes, Margot and Meyer, Christian M. and Gurevych, Iryna}, 
  title = {Bridging the gap between extractive and abstractive summaries: Creation and evaluation of coherent extracts from heterogeneous sources},
  booktitle = {Proceedings of the 26th International Conference on Computational Linguistics (COLING)},
  month = {December},
  year = {2016},
  pages = {1039--1050},
  location = {Osaka, Japan},
  url = {http://www.aclweb.org/anthology/C/C16/C16-1099.pdf}
}
```

> **Abstract:** Coherent extracts are a novel type of summary combining the advantages of manually created abstractive summaries, which are fluent but difficult to evaluate, and low-quality automatically created extractive summaries, which lack coherence and structure. We use a corpus of heterogeneous documents to address the issue that information seekers usually face – a variety of different types of information sources. We directly extract information from these, but minimally redact and meaningfully order it to form a coherent text. Our qualitative and quantitative evaluations show that quantitative results are not sufficient to judge the quality of a summary and that other quality criteria, such as coherence, should also be taken into account. We find that our manually created corpus is of high quality and that it has the potential to bridge the gap between reference corpora of abstracts and automatic methods producing extracts. Our corpus is available to the research community for further development.

## License
The data shared in this repository is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/) (CC-BY-SA). See LICENSE.txt for detailed information. If you use the corpus in academic works, please cite our COLING paper. 

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>

Note that for legal issues, we cannot redistribute the full text of the source documents. Please contact us if you need help with crawling them.  

## Contact
Don't hesitate to send us an e-mail or report an issue, if something is broken (and it shouldn't be) or if you have further questions. Points of contact:

* [Darina Benikova](http://www.is.informatik.uni-duisburg.de/staff/benikova.html)
* [Christian M. Meyer](http://www.ukp.tu-darmstadt.de/people/meyer)
* [Margot Mieskes](https://www.ukp.tu-darmstadt.de/people/former-research-staff/prof-dr-margot-mieskes/)
* [Christopher Tauchmann](https://www.aiphes.tu-darmstadt.de/de/aiphes/people/doctoral-researchers/christopher-tauchmann/)

## Documentation
We provide the DBS corpus in two versions:

* Version 1 consists of the 10 topics described and evaluated in our COLING paper  
	* Folder: **dbs-corpus-v1**
* Version 2 contains the summaries for 20 additional topics (total = 30)
	* Folder: **dbs-corpus-v2**
* All annotations and summaries have been produced using our **[MDS<i>Writer</i> tool](https://github.com/AIPHES/mdswriter)** (available as open-source software!)

Detailed information about the file format

* UTF-8 encoded files in XML and tab separated (TSV) format
	* **The XML and TSV files contain the same data**, so it is enough to process one of these files!
	* The column names below refer to the TSV format, but it should be straight-forward to map them to the XML format. Contact us if you have any problems 
* **dbs-topics** – the list of topics
	* ID: A unique topic ID referenced in the other files
	* TOPIC: The title of this topic
	* NUM_DOCUMENTS: The number of source documents in this topic 
	* SOURCE: The link to the topic page at the [Deutscher Bildungsserver](https://www.bildungsserver.de) (DBS) webpage 
* **dbs-document-links** contains the source documents grouped by topic (not preprocessed)
	* ID: A unique document ID referenced in the other files
	* TOPIC_ID: The ID of the topic as defined in the dbs-topics file
	* TITLE: The title of this document
	* TEXT: For legal reasons, we cannot publish the full text. Contact us for more details!
	* SOURCE: The link to the original webpage the full text has been taken from
* **dbs-highlights** – the results of our first annotation step (i.e., important spans of the source documents)
	* ID: A unique ID of this highlighted text span
	* TOPIC_ID: The ID of the topic as defined in the dbs-topics file
	* DOC_ID: The ID of the document as defined in the dbs-document-links file
	* USER_ID: The ID of the user, who created this highlighted text span
	* POSITION_START, POSITION_END: The character offsets of this highlighted text span in the document's raw full text
	* TEXT: The text that has been highlighted by the user (i.e., the content of the text span)
	* SOURCE: The speaker or source of the text span (in case of reported speech or quotations)
	* LINK_GROUP: An ID number that indicates if two or more highlights belong together (i.e., they have been "linked" and should be merged to a single nugget); -1 means unlinked
    * COLOR: The color (red, yellow, green) a user has assigned to the text span as a running number 
    * NUGGET_ID: The ID of the nugget that contains this highlight as defined in the dbs-nuggets file
* **dbs-nuggets** – the results of our annotation steps 2-6 (i.e., important information nuggets)
	* ID: A unique ID of this nugget
	* TOPIC_ID: The ID of the topic as defined in the dbs-topics file
	* DOC_ID: The ID of the document as defined in the dbs-document-links file
	* USER_ID: The ID of the user, who created this highlighted text span
	* POSITION_START, POSITION_END: The character offsets of this nugget in the document's raw full text; if a nugget consists of multiple highlighted text spans, we provide the minimum of the start offsets and the maximum of the end offsets
	* TEXT: The raw text of the information nugget (i.e., the concatenation of the highlighted text spans, delimited by the … symbol)
	* CONTEXT: The 10 context words to the left and right of the nugget; the texts of the nugget/highlighted text span are replaced by the … symbol 
    * COREF_RESOLVED: The result of annotation step 4: the nugget's text with resolved co-references (only for best nuggets)
    * REVISED_TEXT: The result of annotation step 5: nugget's reformulated text to form a full sentence (only for best nuggets)
	* SOURCE: The speaker or source of the text span (in case of reported speech or quotations)
    * REDUNDANT_CLUSTER: The result of annotation step 2: the clustering of redundant nuggets (same number indicates the same redundancy cluster)
    * REDUNDANT_IS_BEST: The result of annotation step 3: the selection of a single representative per redundancy cluster called the "best nugget" (1 = selected as best nugget, 0 = not selected)
    * COHCLUSTER, COHCLUSTER_NAME, COHCLUSTER_POSITION: The result of annotation step 6: a meaningful order of the nuggets into so-called coherence clusters
	    * Each coherence cluster has a (topic&user-wide) unique ID and a headline
	    * The position of a nugget within the cluster is indicated by a running number in the COHCLUSTER_POSITION field
* **dbs-summaries** – the "coherent extract" summaries compiled in our annotation step 7
	* ID: A unique ID of this summary
	* TOPIC_ID: The ID of the topic as defined in the dbs-topics file
	* USER_ID: The ID of the user, who created this highlighted text span
	* SUMMARY_NR: A running number of the summary (currently always "1")
	* SUMMARY_TEXT: The text of the summary
* **dbs-statistics** – a few basic statistics, such as the number of documents and summaries
    
