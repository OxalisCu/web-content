---
id: product_faq.md
summary: 查找有关世界上最先进的矢量数据库常见问题的答案。
title: 产品常见问题
---
<h1 id="Product-FAQ" class="common-anchor-header">产品常见问题<button data-href="#Product-FAQ" class="anchor-icon" translate="no">
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
    </button></h1><h4 id="How-much-does-Milvus-cost" class="common-anchor-header">Milvus 的成本是多少？</h4><p>Milvus 是一个 100% 免费的开源项目。</p>
<p>在将 Milvus 用于生产或发布目的时，请遵守<a href="http://www.apache.org/licenses/LICENSE-2.0">Apache License 2.0</a>。</p>
<p>Milvus 背后的公司 Zilliz 还为那些不想构建和维护自己的分布式实例的用户提供完全托管的云版平台。<a href="https://zilliz.com/cloud">Zilliz 云平台</a>可自动维护数据的可靠性，用户只需支付使用费用。</p>
<h4 id="Does-Milvus-support-non-x86-architectures" class="common-anchor-header">Milvus 支持非 x86 架构吗？</h4><p>Milvus不能在非x86平台上安装或运行。</p>
<p>您的 CPU 必须支持以下指令集之一，才能运行 Milvus：SSE4.2、AVX、AVX2、AVX512。这些都是 x86 专用 SIMD 指令集。</p>
<h4 id="What-is-the-maximum-dataset-size-Milvus-can-handle" class="common-anchor-header">Milvus 能处理的最大数据集大小是多少？</h4><p>从理论上讲，Milvus 能处理的最大数据集大小取决于其运行的硬件，特别是系统内存和存储：</p>
<ul>
<li>在运行查询之前，Milvus 会将所有指定的集合和分区加载到内存中。因此，内存大小决定了 Milvus 能查询的最大数据量。</li>
<li>当新实体和与集合相关的模式（目前只支持 MinIO 用于数据持久化）被添加到 Milvus 时，系统存储将决定插入数据的最大允许大小。</li>
</ul>
<h4 id="Where-does-Milvus-store-data" class="common-anchor-header">Milvus 在哪里存储数据？</h4><p>Milvus 处理两种类型的数据：插入数据和元数据。</p>
<p>插入数据（包括矢量数据、标量数据和特定于集合的模式）以增量日志的形式存储在持久存储中。Milvus 支持多种对象存储后端，包括<a href="https://min.io/">MinIO</a>、<a href="https://aws.amazon.com/s3/?nc1=h_ls">AWS S3</a>、<a href="https://cloud.google.com/storage?hl=en#object-storage-for-companies-of-all-sizes">谷歌云</a> <a href="https://azure.microsoft.com/en-us/products/storage/blobs">存储</a>（GCS）、<a href="https://azure.microsoft.com/en-us/products/storage/blobs">Azure Blob 存储</a>、<a href="https://www.alibabacloud.com/product/object-storage-service">阿里云 OSS</a> 和<a href="https://www.tencentcloud.com/products/cos">腾讯云对象存储</a>（COS）。</p>
<p>元数据在 Milvus 内部生成。每个 Milvus 模块都有自己的元数据，这些元数据存储在 etcd 中。</p>
<h4 id="Why-is-there-no-vector-data-in-etcd" class="common-anchor-header">为什么 etcd 中没有矢量数据？</h4><p>etcd 存储 Milvus 模块元数据；MinIO 存储实体。</p>
<h4 id="Does-Milvus-support-inserting-and-searching-data-simultaneously" class="common-anchor-header">Milvus 支持同时插入和搜索数据吗？</h4><p>是的。插入操作和查询操作由两个相互独立的模块处理。从客户端的角度来看，当插入的数据进入消息队列时，插入操作就完成了。但是，插入的数据在加载到查询节点之前是不可查询的。如果数据段的大小没有达到建立索引的阈值（默认为 512 MB），Milvus 就会采用暴力搜索，查询性能可能会降低。</p>
<h4 id="Can-vectors-with-duplicate-primary-keys-be-inserted-into-Milvus" class="common-anchor-header">能否在 Milvus 中插入主键重复的向量？</h4><p>可以。Milvus 不会检查矢量主键是否重复。</p>
<h4 id="When-vectors-with-duplicate-primary-keys-are-inserted-does-Milvus-treat-it-as-an-update-operation" class="common-anchor-header">插入主键重复的向量时，Milvus 是否将其视为更新操作？</h4><p>Milvus 目前不支持更新操作，也不检查实体主键是否重复。你有责任确保实体主键是唯一的，如果它们不是唯一的，Milvus 可能包含多个主键重复的实体。</p>
<p>如果出现这种情况，查询时将返回哪个数据副本仍是未知行为。这一限制将在今后的版本中修复。</p>
<h4 id="What-is-the-maximum-length-of-self-defined-entity-primary-keys" class="common-anchor-header">自定义实体主键的最大长度是多少？</h4><p>实体主键必须是非负 64 位整数。</p>
<h4 id="What-is-the-maximum-amount-of-data-that-can-be-added-per-insert-operation" class="common-anchor-header">每次插入操作可添加的最大数据量是多少？</h4><p>插入操作的大小不得超过 1,024 MB。这是 gRPC 规定的限制。</p>
<h4 id="Does-collection-size-impact-query-performance-when-searching-in-a-specific-partition" class="common-anchor-header">在特定分区中搜索时，集合大小会影响查询性能吗？</h4><p>如果为搜索指定了分区，Milvus 只搜索指定的分区。</p>
<h4 id="Does-Milvus-load-the-entire-collection-when-partitions-are-specified-for-a-search" class="common-anchor-header">为搜索指定分区时，Milvus 会加载整个集合吗？</h4><p>不会。Milvus 的行为各不相同。数据必须在搜索前加载到内存中。</p>
<ul>
<li>如果您知道数据位于哪个分区，请调用<code translate="no">load_partition()</code> 加载目标分区，<em>然后</em>在<code translate="no">search()</code> 方法调用中指定分区。</li>
<li>如果不知道确切的分区，请先调用<code translate="no">load_collection()</code> ，然后再调用<code translate="no">search()</code> 。</li>
<li>如果在搜索前没有加载集合或分区，Milvus 会返回错误信息。</li>
</ul>
<h4 id="Can-indexes-be-created-after-inserting-vectors" class="common-anchor-header">插入向量后能否创建索引？</h4><p>可以。如果之前已通过<code translate="no">create_index()</code> 为某个集合建立了索引，Milvus 将自动为随后插入的向量建立索引。不过，在新插入的向量填满整个数据段且新创建的索引文件与之前的索引文件分开之前，Milvus 不会建立索引。</p>
<h4 id="How-are-the-FLAT-and-IVFFLAT-indexes-different" class="common-anchor-header">FLAT 和 IVF_FLAT 索引有何不同？</h4><p>IVF_FLAT 索引将向量空间划分为列表簇。在默认列表值为 16,384 时，Milvus 会比较目标向量与所有 16,384 个簇的中心点之间的距离，以返回最近的探测簇。然后，Milvus 会比较目标向量与选定簇中向量之间的距离，以获得最近的向量。与 IVF_FLAT 不同，FLAT 直接比较目标向量与其他向量之间的距离。</p>
<p>当向量总数约等于 nlist 时，IVF_FLAT 和 FLAT 在计算要求和搜索性能上几乎没有差距。但是，当向量数量超过 nlist 的两倍或更多时，IVF_FLAT 就开始显示出性能优势。</p>
<p>更多信息，请参阅<a href="/docs/zh/index.md">矢量索引</a>。</p>
<h4 id="How-does-Milvus-flush-data" class="common-anchor-header">Milvus 如何刷新数据？</h4><p>当插入的数据加载到消息队列时，Milvus 返回成功。但是，数据尚未刷新到磁盘。然后，Milvus 的数据节点会将消息队列中的数据作为增量日志写入持久存储。如果调用<code translate="no">flush()</code> ，数据节点就会被迫立即将消息队列中的所有数据写入持久化存储。</p>
<h4 id="What-is-normalization-Why-is-normalization-needed" class="common-anchor-header">什么是规范化？为什么需要规范化？</h4><p>归一化是指转换矢量，使其规范等于 1 的过程。如果使用内积来计算向量的相似性，则必须对向量进行归一化。归一化后，内积等于余弦相似度。</p>
<p>更多信息，请参见<a href="https://en.wikipedia.org/wiki/Unit_vector">维基百科</a>。</p>
<h4 id="Why-do-Euclidean-distance-L2-and-inner-product-IP-return-different-results" class="common-anchor-header">为什么欧氏距离（L2）和内积（IP）返回的结果不同？</h4><p>对于归一化向量，欧氏距离 (L2) 在数学上等同于内积 (IP)。如果这些相似度指标返回的结果不同，请检查您的向量是否已归一化。</p>
<h4 id="Is-there-a-limit-to-the-total-number-of-collections-and-partitions-in-Milvus" class="common-anchor-header">Milvus 的集合和分区总数有限制吗？</h4><p>有。在 Milvus 实例中最多可以创建 65,535 个集合。在计算现有集合数量时，Milvus 会计算所有包含分片和分区的集合。</p>
<p>例如，假设您已经创建了 100 个集合，其中 60 个集合有 2 个分块和 4 个分区，其余 40 个集合有 1 个分块和 12 个分区。当前的集合数可以计算为</p>
<pre><code translate="no">60 * 2 * 4 + 40 * 1 * 12 = 960
<button class="copy-code-btn"></button></code></pre>
<h4 id="Why-do-I-get-fewer-than-k-vectors-when-searching-for-topk-vectors" class="common-anchor-header">在搜索<code translate="no">topk</code> 向量时，为什么得到的向量少于 k 个？</h4><p>在 Milvus 支持的索引中，IVF_FLAT 和 IVF_SQ8 实现了 k-means 聚类方法。数据空间被划分为<code translate="no">nlist</code> 个簇，插入的向量被分配到这些簇中。然后，Milvus 会选择<code translate="no">nprobe</code> 最近的簇，并比较目标向量与所选簇中所有向量之间的距离，返回最终结果。</p>
<p>如果<code translate="no">nlist</code> 和<code translate="no">topk</code> 较大，而 nprobe 较小，则 nprobe 簇中的向量数量可能少于<code translate="no">k</code> 。因此，当搜索<code translate="no">topk</code> 最近的向量时，返回的向量数量少于<code translate="no">k</code> 。</p>
<p>为避免这种情况，可尝试将<code translate="no">nprobe</code> 设置得大一些，将<code translate="no">nlist</code> 和<code translate="no">k</code> 设置得小一些。</p>
<p>更多信息，请参阅 "<a href="/docs/zh/index.md">向量索引"</a>。</p>
<h4 id="What-is-the-maximum-vector-dimension-supported-in-Milvus" class="common-anchor-header">Milvus 支持的最大向量维度是多少？</h4><p>Milvus 默认最多可管理 32,768 维的向量。你可以增加<code translate="no">Proxy.maxDimension</code> 的值，以允许更大维度的向量。</p>
<h4 id="Does-Milvus-support-Apple-M1-CPU" class="common-anchor-header">Milvus 支持苹果 M1 CPU 吗？</h4><p>当前的 Milvus 版本不支持苹果 M1 CPU。</p>
<h4 id="What-data-types-does-Milvus-support-on-the-primary-key-field" class="common-anchor-header">Milvus 支持主键字段的哪些数据类型？</h4><p>在当前版本中，Milvus 支持 INT64 和字符串。</p>
<h4 id="Is-Milvus-scalable" class="common-anchor-header">Milvus 可以扩展吗？</h4><p>可以。你可以在 Kubernetes 上通过 Helm Chart 部署多节点的 Milvus 集群。更多说明请参阅《<a href="/docs/zh/scaleout.md">扩展指南》</a>。</p>
<h4 id="Does-the-query-perform-in-memory-What-are-incremental-data-and-historical-data" class="common-anchor-header">查询是否在内存中执行？什么是增量数据和历史数据？</h4><p>是的。当收到查询请求时，Milvus 会将增量数据和历史数据加载到内存中进行搜索。增量数据是不断增长的数据段，它们在达到在存储引擎中持久化的阈值之前会被缓冲到内存中，而历史数据则来自存储在对象存储中的密封数据段。增量数据和历史数据共同构成了要搜索的整个数据集。</p>
<h4 id="Is-Milvus-available-for-concurrent-search" class="common-anchor-header">Milvus 是否支持并发搜索？</h4><p>可以。对于同一数据集的查询，Milvus 会同时搜索增量数据和历史数据。不过，对不同数据集的查询是串联进行的。历史数据可能是一个极其庞大的数据集，因此对历史数据的搜索相对更耗时，而且基本上是串联进行的。</p>
<h4 id="Why-does-the-data-in-MinIO-remain-after-the-corresponding-collection-is-dropped" class="common-anchor-header">为什么 MinIO 中的数据会在相应的数据集被删除后保留下来？</h4><p>MinIO 中的数据被设计为保留一段时间，以方便数据回滚。</p>
<h4 id="Does-Milvus-support-message-engines-other-than-Pulsar" class="common-anchor-header">除了 Pulsar 之外，Milvus 还支持其他消息引擎吗？</h4><p>支持。Milvus 2.1.0 支持 Kafka。</p>
<h4 id="Whats-the-difference-between-a-search-and-a-query" class="common-anchor-header">搜索和查询有什么区别？</h4><p>在 Milvus 中，向量相似性搜索基于相似性计算和向量索引加速来检索向量。与矢量相似性搜索不同，矢量查询是通过基于布尔表达式的标量过滤来检索矢量的。布尔表达式会对标量字段或主键字段进行过滤，并检索所有符合过滤条件的结果。在查询中，既不涉及相似度指标，也不涉及向量索引。</p>
<h4 id="Why-does-a-float-vector-value-have-a-precision-of-7-decimal-digits-in-Milvus" class="common-anchor-header">为什么在 Milvus 中，浮点矢量值的精度是小数点后 7 位？</h4><p>Milvus 支持将向量存储为 Float32 数组。Float32 值的精度为小数点后 7 位。即使是 Float64 值，如 1.3476964684980388，Milvus 也将其存储为 1.347696。因此，当你从 Milvus 中检索这样一个向量时，Float64 值的精度就会丢失。</p>
<h4 id="How-does-Milvus-handle-vector-data-types-and-precision" class="common-anchor-header">Milvus 如何处理向量数据类型和精度？</h4><p>Milvus 支持二进制、Float32、Float16 和 BFloat16 向量类型。</p>
<ul>
<li>二进制向量：将二进制数据存储为 0 和 1 的序列，用于图像处理和信息检索。</li>
<li>Float32 向量：默认存储精度约为十进制 7 位数。即使是 Float64 值，也是以 Float32 精度存储的，因此在检索时可能会丢失精度。</li>
<li>Float16 和 BFloat16 向量：可降低精度和内存使用量。Float16 适用于带宽和存储有限的应用，而 BFloat16 则兼顾了范围和效率，常用于深度学习，在不显著影响精度的情况下降低计算要求。</li>
</ul>
<h4 id="Does-Milvus-support-specifying-default-values-for-scalar-or-vector-fields" class="common-anchor-header">Milvus 是否支持为标量或矢量字段指定默认值？</h4><p>目前，Milvus 2.4.x 不支持为标量或矢量字段指定默认值。该功能计划在未来版本中推出。</p>
<h4 id="Still-have-questions" class="common-anchor-header">仍有问题？</h4><p>您可以</p>
<ul>
<li>查看 GitHub 上的<a href="https://github.com/milvus-io/milvus/issues">Milvus</a>。欢迎提出问题、分享想法并帮助他人。</li>
<li>加入我们的<a href="https://slack.milvus.io/">Slack 社区</a>，寻求支持并参与我们的开源<a href="https://slack.milvus.io/">社区</a>。</li>
</ul>