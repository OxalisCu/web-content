---
id: overview.md
title: What is Milvus
related_key: Milvus Overview
summary: >-
  Milvus is an open-source vector database designed specifically for AI
  application development, embeddings similarity search, and MLOps.
---
<h1 id="Introduction" class="common-anchor-header">Introduction<button data-href="#Introduction" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h1><p>This page aims to give you an overview of Milvus by answering several questions. After reading this page, you will learn what Milvus is and how it works, as well as the key concepts, why use Milvus, supported indexes and metrics, example applications, the architecture, and relevant tools.</p>
<h2 id="What-is-Milvus-vector-database" class="common-anchor-header">What is Milvus vector database?<button data-href="#What-is-Milvus-vector-database" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Milvus was created in 2019 with a singular goal: store, index, and manage massive <a href="#Embedding-vectors">embedding vectors</a> generated by deep neural networks and other machine learning (ML) models.</p>
<p>As a database specifically designed to handle queries over input vectors, it is capable of indexing vectors on a trillion scale. Unlike existing relational databases which mainly deal with structured data following a pre-defined pattern, Milvus is designed from the bottom-up to handle embedding vectors converted from <a href="#Unstructured-data">unstructured data</a>.</p>
<p>As the Internet grew and evolved, unstructured data became more and more common, including emails, papers, IoT sensor data, Facebook photos, protein structures, and much more. In order for computers to understand and process unstructured data, these are converted into vectors using embedding techniques. Milvus stores and indexes these vectors. Milvus is able to analyze the correlation between two vectors by calculating their similarity distance. If the two embedding vectors are very similar, it means that the original data sources are similar as well.</p>
<p>
  <span class="img-wrapper">
    <img translate="no" src="/docs/v2.0.x/assets/milvus_workflow.jpeg" alt="Workflow" class="doc-image" id="workflow" />
    <span>Workflow</span>
  </span>
</p>
<h2 id="Key-concepts" class="common-anchor-header">Key concepts<button data-href="#Key-concepts" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>In case you are new to the world of vector database and similarity search, read the following explanation of key concepts to gain a better understanding.</p>
<p>Learn more about <a href="/docs/fr/glossary.md">Milvus glossary</a>.</p>
<h3 id="Unstructured-data" class="common-anchor-header">Unstructured data</h3><p>Unstructured data, including images, video, audio, and natural language, is information that doesn’t follow a predefined model or manner of organization. This data type accounts for ~80% of the world’s data, and can be converted into vectors using various artificial intelligence (AI) and machine learning (ML) models.</p>
<h3 id="Embedding-vectors" class="common-anchor-header">Embedding vectors</h3><p>An embedding vector is a feature abstraction of unstructured data, such as emails, IoT sensor data, Instagram photos, protein structures, and much more. Mathematically speaking, an embedding vector is an array of floating-point numbers or binaries. Modern embedding techniques are used to convert unstructured data to embedding vectors.</p>
<h3 id="Vector-similarity-search" class="common-anchor-header">Vector similarity search</h3><p>Vector similarity search is the process of comparing a vector to a database to find vectors that are most similar to the query vector. Approximate nearest neighbor (ANN) search algorithms are used to accelerate the searching process. If the two embedding vectors are very similar, it means that the original data sources are similar as well.</p>
<h2 id="Why-Milvus" class="common-anchor-header">Why Milvus?<button data-href="#Why-Milvus" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><ul>
<li>High performance when conducting vector search on massive datasets.</li>
<li>A developer-first community that offers multi-language support and toolchain.</li>
<li>Cloud scalability and high reliability even in the event of a disruption.</li>
<li>Hybrid search achieved by pairing scalar filtering with vector similarity search.</li>
</ul>
<h2 id="What-indexes-and-metrics-are-supported" class="common-anchor-header">What indexes and metrics are supported?<button data-href="#What-indexes-and-metrics-are-supported" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Indexes are an organization unit of data. You must declare the index type and similarity metric before you can search or query inserted entities. <strong>If you do not specify an index type, Milvus will operate brute-force search by default.</strong></p>
<h3 id="Index-types" class="common-anchor-header">Index types</h3><p>Most of the vector index types supported by Milvus use approximate nearest neighbors search (ANNS), including:</p>
<ul>
<li><strong>FLAT</strong>: FLAT is best suited for scenarios that seeks perfectly accurate and exact search results on a small, million-scale dataset.</li>
<li><strong>IVF_FLAT</strong>: IVF_FLAT is a quantization-based index and is best suited for scenarios that seeks an ideal balance between accuracy and query speed.</li>
<li><strong>IVF_SQ8</strong>: IVF_SQ8 is a quantization-based index and is best suited for scenarios that seeks a significant reduction on disk, CPU, and GPU memory consumption as these resources are very limited.</li>
<li><strong>IVF_PQ</strong>: IVF_PQ is a quantization-based index and is best suited for scenarios that seeks high query speed even at the cost of accuracy.</li>
<li><strong>HNSW</strong>: HNSW is a graph-based index and is best suited for scenarios that has a high demand for search efficiency.</li>
<li><strong>ANNOY</strong>: ANNOY is a tree-based index and is best suited for scenarios that seeks a high recall rate.</li>
</ul>
<p>See <a href="/docs/fr/index.md">Vector Index</a> for more details.</p>
<h3 id="Similarity-metrics" class="common-anchor-header">Similarity metrics</h3><p>In Milvus, similarity metrics are used to measure similarities among vectors. Choosing a good distance metric helps improve classification and clustering performance significantly. Depending on the input data forms, specific similarity metric is selected for optimal performance.</p>
<p>The metrics that are widely used for floating-point embeddings include:</p>
<ul>
<li><strong>Euclidean distance (L2)</strong>: This metric is generally used in the field of computer vision (CV).</li>
<li><strong>Inner product (IP)</strong>: This metric is generally used in the field of natural language processing (NLP).
The metrics that are widely used for binary embeddings include:</li>
<li><strong>Hamming</strong>: This metric is generally used in the field of natural language processing (NLP).</li>
<li><strong>Jaccard</strong>: This metric is generally used in the field of molecular similarity search.</li>
<li><strong>Tanimoto</strong>: This metric is generally used in the field of molecular similarity search.</li>
<li><strong>Superstructure</strong>: This metric is generally used to search for similar superstructure of a molecule.</li>
<li><strong>Substructure</strong>: This metric is generally used  to search for similar substructure of a molecule.</li>
</ul>
<p>See <a href="/docs/fr/metric.md#floating">Similarity Metrics</a> for more information.</p>
<h2 id="Example-applications" class="common-anchor-header">Example applications<button data-href="#Example-applications" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Milvus makes it easy to add similarity search to your applications. Example applications of Milvus include:</p>
<ul>
<li><a href="/docs/fr/image_similarity_search.md">Image similarity search</a>: Images made searchable and instantaneously return the most similar images from a massive database.</li>
<li><a href="/docs/fr/video_similarity_search.md">Video similarity search</a>: By converting key frames into vectors and then feeding the results into Milvus, billions of videos can be searched and recommended in near real time.</li>
<li><a href="/docs/fr/audio_similarity_search.md">Audio similarity search</a>: Quickly query massive volumes of audio data such as speech, music, sound effects, and surface similar sounds.</li>
<li><a href="/docs/fr/molecular_similarity_search.md">Molecular similarity search</a>: Blazing fast similarity search, substructure search, or superstructure search for a specified molecule.</li>
<li><a href="/docs/fr/recommendation_system.md">Recommender system</a>: Recommend information or products based on user behaviors and needs.</li>
<li><a href="/docs/fr/question_answering_system.md">Question answering system</a>: Interactive digital QA chatbot that automatically answers user questions.</li>
<li><a href="/docs/fr/dna_sequence_classification.md">DNA sequence classification</a>: Accurately sort out the classification of a gene in milliseconds by comparing similar DNA sequence.</li>
<li><a href="/docs/fr/text_search_engine.md">Text search engine</a>: Help users find the information they are looking for by comparing keywords against a database of texts.</li>
</ul>
<p>See <a href="https://github.com/milvus-io/bootcamp/tree/master/solutions">Milvus tutorials</a> and <a href="/docs/fr/milvus_adopters.md">Milvus Adopters</a> for more Milvus application scenarios.</p>
<h2 id="How-is-Milvus-designed" class="common-anchor-header">How is Milvus designed?<button data-href="#How-is-Milvus-designed" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>As a cloud-native vector database, Milvus 2.0 separates storage and computation by design. To enhance elasticity and flexibility, all components in Milvus 2.0 are stateless.</p>
<p>The system breaks down into four levels:</p>
<ul>
<li>Access layer: The access layer is composed of a group of stateless proxies and serves as the front layer of the system and endpoint to users.</li>
<li>Coordinator service: The coordinator service assigns tasks to the worker nodes and functions as the system’s brain.</li>
<li>Worker nodes: The worker nodes function as arms and legs and are dumb executors that follow instructions from the coordinator service and execute user-triggerd DML/DDL commands.</li>
<li>Storage: Storage is the bone of the system, and is responsible for data persistence. It comprises meta storage, log broker, and object storage.</li>
</ul>
<p>For more information, see <a href="/docs/fr/architecture_overview.md">Architecture Overview</a>.</p>
<p>
  <span class="img-wrapper">
    <img translate="no" src="/docs/v2.0.x/assets/architecture_02.jpg" alt="Architecture" class="doc-image" id="architecture" />
    <span>Architecture</span>
  </span>
</p>
<h2 id="Developer-tools" class="common-anchor-header">Developer tools<button data-href="#Developer-tools" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Milvus is supported by rich APIs and tools to facilitate DevOps.</p>
<h3 id="API-access" class="common-anchor-header">API access</h3><p>Milvus has client libraries wrapped on top of the Milvus API that can be used to insert, delete, and query data programmatically from application code:</p>
<ul>
<li><a href="https://github.com/milvus-io/pymilvus">PyMilvus</a></li>
<li><a href="https://github.com/milvus-io/milvus-sdk-node">Node.js SDK</a></li>
<li><a href="https://github.com/milvus-io/milvus-sdk-go">Go SDK</a></li>
</ul>
<p>We are working on enabling more new client libraries. If you would like to contribute, go to the corresponding repository of <a href="https://github.com/milvus-io">the Milvus Project</a>.</p>
<h3 id="Milvus-ecosystem-tools" class="common-anchor-header">Milvus ecosystem tools</h3><p>The Milvus ecosystem provides helpful tools including:</p>
<ul>
<li><a href="https://github.com/milvus-io/milvus_cli#overview">Milvus CLI</a></li>
<li><a href="https://github.com/zilliztech/attu">Attu</a>, a graphical management system for Milvus.</li>
<li><a href="/docs/fr/migrate_overview.md">MilvusDM</a> (Milvus Data Migration), an open-source tool designed specifically for importing and exporting data with Milvus.</li>
<li><a href="https://milvus.io/tools/sizing/">Milvus sizing tool</a>, which helps you estimate the raw file size, memory size, and stable disk size needed for a specified number of vectors with various index types.</li>
</ul>
<h2 id="Whats-next" class="common-anchor-header">What’s next<button data-href="#Whats-next" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><ul>
<li>Get started with a 3-minute tutorial:
<ul>
<li><a href="/docs/fr/example_code.md">Hello Milvus</a></li>
</ul></li>
<li>Install Milvus for your testing or production environment:
<ul>
<li><a href="/docs/fr/prerequisite-docker.md">Installation Prerequisites</a></li>
<li><a href="/docs/fr/install_standalone-docker.md">Install Milvus Standalone</a></li>
<li><a href="/docs/fr/install_cluster-docker.md">Install Milvus Cluster</a></li>
</ul></li>
<li>If you’re interested in diving deep into the design details of Milvus:
<ul>
<li>Read about <a href="/docs/fr/architecture_overview.md">Milvus architecture</a></li>
</ul></li>
</ul>