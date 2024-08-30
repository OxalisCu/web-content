---
id: milvusdm_install.md
summary: Learn how to install MilvusDM to migrate your data.
title: Install MilvusDM
---
<h1 id="Install-MilvusDM" class="common-anchor-header">Install MilvusDM<button data-href="#Install-MilvusDM" class="anchor-icon" translate="no">
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
    </button></h1><p>MilvusDM is an open-source tool designed specifically for importing and exporting data with Milvus. This page shows you how to install MilvusDM.</p>
<div class="alert note">
  The pymilvusdm2.0 is used for migrating data <b>from Milvus(0.10.x or 1.x) to Milvus2.x</b>.
</div>
<h2 id="Before-you-begin" class="common-anchor-header">Before you begin<button data-href="#Before-you-begin" class="anchor-icon" translate="no">
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
    </button></h2><p>Ensure you meet the requirements for operating system and software before installing MilvusDM.</p>
<table>
<thead>
<tr><th>Operating system</th><th>Supported versions</th></tr>
</thead>
<tbody>
<tr><td>CentOS</td><td>7.5 or higher</td></tr>
<tr><td>Ubuntu LTS</td><td>18.04 or higher</td></tr>
</tbody>
</table>
<table>
<thead>
<tr><th>Software</th><th>Version</th></tr>
</thead>
<tbody>
<tr><td><a href="https://milvus.io/">Milvus</a></td><td>0.10.x or 1.x or 2.x</td></tr>
<tr><td>Python3</td><td>3.7 or higher</td></tr>
<tr><td>pip3</td><td>Should be in correspondence to the Python version.</td></tr>
</tbody>
</table>
<h2 id="Install-MilvusDM" class="common-anchor-header">Install MilvusDM<button data-href="#Install-MilvusDM" class="anchor-icon" translate="no">
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
    </button></h2><ol>
<li>Add the following two lines to the <strong>~/.bashrc</strong> file:</li>
</ol>
<pre><code translate="no" class="language-bash"><span class="hljs-keyword">export</span> <span class="hljs-variable constant_">MILVUSDM_PATH</span>=<span class="hljs-string">&#x27;/home/$user/milvusdm&#x27;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">LOGS_NUM</span>=<span class="hljs-number">0</span>
<button class="copy-code-btn"></button></code></pre>
<ul>
<li><p><code translate="no">MILVUSDM_PATH</code>: This parameter defines the working path of MilvusDM. Logs and data generated by MilvusDM will be stored in this path.  The default value is <code translate="no">/home/$user/milvusdm</code>.</p></li>
<li><p><code translate="no">LOGS_NUM</code>： MilvusDM generates one log file each day. This parameter defines the number of log files you would like to save. The default value is 0, which means all log files are saved.</p></li>
</ul>
<ol start="2">
<li>Configure environment variables：</li>
</ol>
<pre><code translate="no" class="language-shell">$ <span class="hljs-built_in">source</span> ~/.bashrc
<button class="copy-code-btn"></button></code></pre>
<ol start="3">
<li>Install MilvusDM with <code translate="no">pip</code>:</li>
</ol>
<pre><code translate="no" class="language-shell">$ pip3 install pymilvusdm==2.0
<button class="copy-code-btn"></button></code></pre>