# NERP-MultiSearch 
<p align="center"><img src="https://github.com/semantic-search/indexing_main/raw/master/nERP.png" width="200" height="200" alt="project-image"></p>
Neural Information Extraction, Retrieval, and Processing for Multi-Modal Neural Search

## Introduction

This project proposes an architecture for efficiently and securely extracting, processing, and searching for information from digital media through the use of deep learning approaches. The architecture is designed to make digital content more accessible through semantic search and explore the domains of information extraction from digital media.

## Keywords

-   Neural Search
-   Information Retrieval
-   Semantic Search

## Proposed Architecture and Approaches

The proposed architecture consists of three serving layers: extraction, transformation, and loading.

### Extraction

The extraction phase retrieves data from various sources (e.g. cloud storage, databases, websites) and categorizes it based on its MIME type (e.g. document, audio/video, image). Necessary text and images are extracted and stored in a document database, while extracted images are passed to the transformation phase for further processing. The extraction phase also involves the creation of a config.yaml file, which contains configurations for various file types and information retrieval techniques.

-   Document extraction: Extracting data (text and images) from document types such as .doc, .ppt, .xls, and .pdf
-   Video extraction: Extracting video frames and audio and storing them separately
-   Web-page extraction: Parsing HTML to extract text and image data from websites

### Transformation Phase

The transformation phase converts raw data from the extraction phase into a normalized format and stores it using an asynchronous task distributed system (e.g. Apache Kafka, Redis). It consists of three blocks: audio transformation, image transformation, and video transformation. Tools like OpenCV and Pillow may be used for image and video processing.

The transformation phase also includes a consumer block with worker nodes that listen to queues and process incoming tasks. These workers have the ability to act as producers, triggering additional tasks and chaining them together. The producer block consists of web nodes that handle web requests and enqueue jobs in the task queue when a new task is received. The task queue, implemented using a Redis transport, acts as the broker, controlling the flow of information into the system and storing tasks temporarily in case of system failure.

### Loading

The loading phase performs the important processes of information retrieval and indexing, and provides an abstraction layer for searching through all indexed data. The process of indexing begins with the creation of a config.yaml file, which specifies the deep learning-based information retrieval techniques and containers to be used for processing.

A single task goes through the following procedures:

1.  Downloading a single file or retrieving it from cloud storage, a binary storage database, or an API
2.  Parsing the binary or file metadata to determine the MIME type and categorizing the file accordingly
3.  Starting the necessary containers for information retrieval based on the config.yaml file and the file's MIME type
4.  Extracting relevant information from the file using the specified information retrieval techniques
5.  Indexing the extracted information for searching

## Searching
The search phase of the implementation allows users to search indexed data using four methods: text search with semantic search and full-text search, audio search using audio fingerprinting, image-to-image search using Euclidean distance, and face search using facial vectors and the Dlib library. Text search uses BERT and Elasticsearch, while full-text search uses Typesense. Image search uses Xception. The search process starts when a client sends a request to the API Gateway, which routes the request to the appropriate microservice.

## Conclusion

This architecture presents a solution for efficiently extracting, processing, and searching for information from digital media through the use of deep learning techniques and an asynchronous task distributed system. It aims to make digital content more accessible through semantic search and improve the process of indexing and storing large amounts of digital media.

## Demos
### Image Caption Search
Search images based on senetences, phrases or captions

![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture1.png)
### Reverse Image Search
Search similar images based on uploaded images

![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture2.png)

### Elastic Search with BERT
Search documents with similar meaning using bert vectorization over elastic search

![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture3.png)

### Face Search
Search similar persons based on facial data using face-to-face search

![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture4.png)
### Ocr
Search images using ocr text
![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture9.png)
### Typo-Tolerant Search
Search millions of documents within seconds with type errors using typo-tolerant-search
![enter image description here](https://github.com/semantic-search/indexing_main/raw/master/demos/Picture11.png)

## Citation
```BibTeX
@InProceedings{10.1007/978-981-19-0898-9_8,
author="Gosaliya, Jainal S.
and Gupta, Adarsh K.
and Ashok, Akshay
and Parikh, Swapnil M.",
editor="Pandian, A. Pasumpon
and Fernando, Xavier
and Haoxiang, Wang",
title="Architectural Insight of Neural Information Extraction, Retrieval, and Processing for Multimodal Neural Search",
booktitle="Computer Networks, Big Data and IoT",
year="2022",
publisher="Springer Nature Singapore",
address="Singapore",
pages="93--110",
abstract="In the growing world of digitization, digital media is engendered in abundance. With the ascension of the utilization of the Internet, there has been a prodigious increase in the engendering of digital content which includes images, audio, video, and documents such as pdf and text data. Information is free and more accessible than in any other era of humanity. Due to such a cognizance explosion, there is a vigorous need to make it more accessible. This can be achieved with semantic search. The quandary of processing, indexing, and storing such content has grown exponentially. At the same time, the infrastructure to handle such length has to be efficient and scalable. The current scenario of erudition explosion resulted in sizably voluminous data having a high performant scalable and resilient architecture which can parallelly process this multimodal binary file, can be gamely transmuting, and is becoming a requirement of the future. Different from the subsisting approaches that design handcrafted and task-concrete architectures for neural search to address only a single task, our architecture is tuned to handle multimodality which fundamentally denotes those data types (modalities) that can be audio, video, documents, images. This paper discusses the solution available to make digital content more accessible which is engendered as a result of the cognizance explosion. The proposed architecture will explore the domains of information extraction from this digital media securely and efficiently with various deep learning approaches for some categorical use cases.",
isbn="978-981-19-0898-9"
}
