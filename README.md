## Docker. Explained.

This Readme file provides the main key points about the what the Dockers are and how they can be used in MlOPS, DevOps, and in Data science.

### What are Containers?
<p>A group of processes run on isolation.
<ul>
  <li>All processes must be able to run on the shared kernel.</li>
</ul></p>

<p>Each container has its own set of <b>namespaces</b> (<i>isolated view</i>):
<ul>
  <li><code>PID</code> - process IDs.</li>
  <li><code>USER</code> - user and group IDs.</li>
  <li><code>UTS</code> - hostname and domain name.</li>
  <li><code>NS</code> - mount points.</li>
  <li><code>NET</code> - network devices, stacks, ports.</li>
  <li><code>IPC</code> - inter-process communications, message queues.</li>
</ul>
</p>
