---
id: operational_faq.md
summary: 查找有关米尔沃斯运营的常见问题的答案。
title: 操作常见问题
---
<h1 id="Operational-FAQ" class="common-anchor-header">操作常见问题<button data-href="#Operational-FAQ" class="anchor-icon" translate="no">
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
    </button></h1><h4 id="What-if-I-failed-to-pull-the-Milvus-Docker-image-from-Docker-Hub" class="common-anchor-header">如果我无法从 Docker Hub 提取 Milvus Docker 镜像怎么办？</h4><p>如果从 Docker Hub 拉取 Milvus Docker 镜像失败，请尝试添加其他注册镜像。</p>
<p>中国大陆的用户可以在<strong>/etc.docker/daemon.json</strong> 中的 registry-mirrors 数组中添加网址 "https://registry.docker-cn.com"。</p>
<pre><code translate="no">{
  <span class="hljs-string">&quot;registry-mirrors&quot;</span>: [<span class="hljs-string">&quot;https://registry.docker-cn.com&quot;</span>]
}
<button class="copy-code-btn"></button></code></pre>
<h4 id="Is-Docker-the-only-way-to-install-and-run-Milvus" class="common-anchor-header">Docker 是安装和运行 Milvus 的唯一方式吗？</h4><p>Docker 是部署 Milvus 的有效方法，但不是唯一的方法。你也可以从源代码部署 Milvus。这需要 Ubuntu（18.04 或更高版本）或 CentOS（7 或更高版本）。更多信息，请参阅<a href="https://github.com/milvus-io/milvus#build-milvus-from-source-code">从源代码构建 Milvus</a>。</p>
<h4 id="What-are-the-main-factors-affecting-recall" class="common-anchor-header">影响召回率的主要因素是什么？</h4><p>召回率主要受索引类型和搜索参数的影响。</p>
<p>对于 FLAT 索引，Milvus 在集合内进行穷举扫描，100% 返回。</p>
<p>对于 IVF 索引，nprobe 参数决定了在集合内的搜索范围。增加 nprobe 会增加搜索向量的比例和召回率，但会降低查询性能。</p>
<p>对于 HNSW 索引，ef 参数决定图搜索的广度。增加 ef 会增加在图上搜索的点数和召回率，但会降低查询性能。</p>
<p>有关详细信息，请参阅<a href="https://www.zilliz.com/blog/Accelerating-Similarity-Search-on-Really-Big-Data-with-Vector-Indexing">矢量索引</a>。</p>
<h4 id="Why-did-my-changes-to-the-configuration-files-not-take-effect" class="common-anchor-header">为什么我对配置文件的修改没有生效？</h4><p>Milvus 不支持在运行期间修改配置文件。必须重新启动 Milvus Docker，配置文件的更改才能生效。</p>
<h4 id="How-do-I-know-if-Milvus-has-started-successfully" class="common-anchor-header">我如何知道 Milvus 是否已成功启动？</h4><p>如果使用 Docker Compose 启动 Milvus，请运行<code translate="no">docker ps</code> 观察有多少 Docker 容器在运行，并检查 Milvus 服务是否正确启动。</p>
<p>对于单机版 Milvus，你应该至少能观察到三个正在运行的 Docker 容器，其中一个是 Milvus 服务，另外两个是 etcd 管理和存储服务。更多信息，请参阅<a href="/docs/zh/install_standalone-docker.md">安装 Milvus 单机版</a>。</p>
<h4 id="Why-is-the-time-in-the-log-files-different-from-the-system-time" class="common-anchor-header">为什么日志文件中的时间与系统时间不同？</h4><p>时间不同通常是由于主机不使用协调世界时（UTC）。</p>
<p>Docker 映像中的日志文件默认使用 UTC。如果您的主机不使用 UTC，可能会出现这个问题。</p>
<h4 id="How-do-I-know-if-my-CPU-supports-Milvus" class="common-anchor-header">我如何知道我的 CPU 是否支持 Milvus？</h4><p>Milvus 的计算操作取决于 CPU 对 SIMD（单指令、多数据）扩展指令集的支持。您的中央处理器是否支持 SIMD 扩展指令集对 Milvus 中的索引构建和矢量相似性搜索至关重要。确保 CPU 至少支持以下一种 SIMD 指令集：</p>
<ul>
<li>SSE4.2</li>
<li>AVX</li>
<li>AVX2</li>
<li>AVX512</li>
</ul>
<p>运行 lscpu 命令检查 CPU 是否支持上述 SIMD 指令集：</p>
<pre><code translate="no">$ lscpu | grep -e sse4_2 -e avx -e avx2 -e avx512
<button class="copy-code-btn"></button></code></pre>
<h4 id="Why-does-Milvus-return-illegal-instruction-during-startup" class="common-anchor-header">为什么 Milvus 在启动时返回<code translate="no">illegal instruction</code> ？</h4><p>Milvus 要求 CPU 支持 SIMD 指令集：SSE4.2、AVX、AVX2 或 AVX512。CPU 必须至少支持其中之一，以确保 Milvus 正常运行。启动过程中返回的<code translate="no">illegal instruction</code> 错误说明 CPU 不支持上述四种指令集中的任何一种。</p>
<p>请参阅<a href="/docs/zh/prerequisite-docker.md">CPU 对 SIMD 指令集的支持</a>。</p>
<h4 id="Can-I-install-Milvus-on-Windows" class="common-anchor-header">我可以在 Windows 上安装 Milvus 吗？</h4><p>可以。你可以通过源代码编译或二进制包在 Windows 上安装 Milvus。</p>
<p>请参阅<a href="https://milvus.io/blog/2021-11-19-run-milvus-2.0-on-windows.md">在 Windows 上运行 Milvus</a>了解如何在 Windows 上安装 Milvus。</p>
<h4 id="I-got-an-error-when-installing-pymilvus-on-Windows-What-shall-I-do" class="common-anchor-header">我在 Windows 上安装 pymilvus 时出错了。我该怎么办？</h4><p>不建议在 Windows 上安装 PyMilvus。但如果您必须在 Windows 上安装 PyMilvus，却发现了错误，请尝试在<a href="https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html">Conda</a>环境中安装。有关如何在 Conda 环境中安装<a href="/docs/zh/install-pymilvus.md">PyMilvus</a>的详细信息，请参阅<a href="/docs/zh/install-pymilvus.md">安装 Milvus SDK</a>。</p>
<h4 id="Can-I-deploy-Milvus-when-disconnected-from-the-Internet" class="common-anchor-header">断开网络连接后还能部署 Milvus 吗？</h4><p>可以。您可以在离线环境中安装 Milvus。更多信息，请参阅<a href="/docs/zh/install_offline-helm.md">离线安装 Milvus</a>。</p>
<h4 id="Where-can-I-find-the-logs-generated-by-Milvus" class="common-anchor-header">在哪里可以找到 Milvus 生成的日志？</h4><p>Milvus 日志默认打印到 stout（标准输出）和 stderr（标准错误），但我们强烈建议在生产中将日志重定向到持久卷。为此，请更新<strong>milvus.yaml</strong> 中的<code translate="no">log.file.rootPath</code> 。如果使用<code translate="no">milvus-helm</code> 图表部署 Milvus，还需要先通过<code translate="no">--set log.persistence.enabled=true</code> 启用日志持久性。</p>
<p>如果你没有更改配置，使用 kubectl logs &lt;pod-name&gt; 或 docker logs CONTAINER 也能帮你找到日志。</p>
<h4 id="Can-I-create-index-for-a-segment-before-inserting-data-into-it" class="common-anchor-header">在插入数据之前，我可以为段创建索引吗？</h4><p>可以。但我们建议在为每个数据段创建索引之前，分批插入数据，每批不应超过 256 MB。</p>
<h4 id="Can-I-share-an-etcd-instance-among-multiple-Milvus-instances" class="common-anchor-header">能否在多个 Milvus 实例之间共享一个 etcd 实例？</h4><p>可以，你可以在多个 Milvus 实例之间共享一个 etcd 实例。为此，在启动每个 Milvus 实例之前，需要在每个实例的配置文件中将<code translate="no">etcd.rootPath</code> 更改为单独的值。</p>
<h4 id="Can-I-share-a-Pulsar-instance-among-multiple-Milvus-instances" class="common-anchor-header">能否在多个 Milvus 实例之间共享一个 Pulsar 实例？</h4><p>可以，你可以在多个 Milvus 实例之间共享一个 Pulsar 实例。为此，你可以</p>
<ul>
<li>如果你的 Pulsar 实例启用了多租户，考虑为每个 Milvus 实例分配一个单独的租户或命名空间。为此，需要在启动 Milvus 实例之前，将其配置文件中的<code translate="no">pulsar.tenant</code> 或<code translate="no">pulsar.namespace</code> 改为每个实例的唯一值。</li>
<li>如果不打算在 Pulsar 实例上启用多租户功能，请考虑在启动 Milvus 实例之前，将其配置文件中的<code translate="no">msgChannel.chanNamePrefix.cluster</code> 更改为每个实例的唯一值。</li>
</ul>
<h4 id="Can-I-share-a-MinIO-instance-among-multiple-Milvus-instances" class="common-anchor-header">我可以在多个 Milvus 实例之间共享 MinIO 实例吗？</h4><p>可以，您可以在多个 Milvus 实例之间共享 MinIO 实例。为此，您需要在启动每个 Milvus 实例之前，在每个实例的配置文件中将<code translate="no">minio.rootPath</code> 更改为唯一值。</p>
<h4 id="How-do-I-handle-the-error-message-pymilvusexceptionsConnectionConfigException-ConnectionConfigException-code1-messageIllegal-uri-exampledb-expected-form-httpsuserpwdexamplecom12345" class="common-anchor-header">如何处理<code translate="no">pymilvus.exceptions.ConnectionConfigException: &lt;ConnectionConfigException: (code=1, message=Illegal uri: [example.db], expected form 'https://user:pwd@example.com:12345')&gt;</code> 错误信息？</h4><p>错误信息<code translate="no">Illegal uri [example.db]</code> 表明你正在尝试使用早期版本的 PyMilvus 连接 Milvus Lite，而早期版本的 PyMilvus 不支持这种连接类型。要解决这个问题，请将 PyMilvus 升级到至少 2.4.2 版本，该版本支持连接 Milvus Lite。</p>
<p>您可以使用以下命令升级 PyMilvus：</p>
<pre><code translate="no" class="language-shell">pip install pymilvus&gt;=2.4.2
<button class="copy-code-btn"></button></code></pre>
<h4 id="Why-am-I-getting-fewer-results-than-the-limit-I-set-in-my-searchquery" class="common-anchor-header">为什么我得到的结果少于我在搜索/查询中设置的<code translate="no">limit</code> ？</h4><p>有几种原因可能导致您收到的结果少于您指定的<code translate="no">limit</code> ：</p>
<ul>
<li><p><strong>数据有限</strong>：集合中可能没有足够的实体来满足您要求的限制。如果集合中的实体总数少于限制，您收到的结果自然会减少。</p></li>
<li><p><strong>主键重复</strong>：在搜索过程中遇到主键重复时，Milvus 会优先处理特定实体。这种行为根据搜索类型而有所不同：</p></li>
<li><p><strong>查询（完全匹配）</strong>：Milvus 选择具有匹配 PK 的最新实体。 ANN 搜索：即使实体共享相同的 PK，Milvus 也会选择相似度得分最高的实体。 如果您的集合有很多重复的主键，这种优先级可能会导致唯一结果少于限制。</p></li>
<li><p><strong>匹配不足</strong>：您的搜索过滤表达式可能过于严格，导致符合相似性阈值的实体较少。如果为搜索设置的条件过于严格，匹配的实体就不够多，导致结果比预期的少。</p></li>
</ul>
<h4 id="Still-have-questions" class="common-anchor-header">还有问题？</h4><p>可以：</p>
<ul>
<li>在 GitHub 上查看<a href="https://github.com/milvus-io/milvus/issues">Milvus</a>。随时提问、分享想法并帮助他人。</li>
<li>加入我们的<a href="https://discuss.milvus.io/">Milvus 论坛</a>或<a href="https://join.slack.com/t/milvusio/shared_invite/enQtNzY1OTQ0NDI3NjMzLWNmYmM1NmNjOTQ5MGI5NDhhYmRhMGU5M2NhNzhhMDMzY2MzNDdlYjM5ODQ5MmE3ODFlYzU3YjJkNmVlNDQ2ZTk">Slack 频道</a>，寻求支持并参与我们的开源社区。</li>
</ul>