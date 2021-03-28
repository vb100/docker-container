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
<code>cgroups</code> controls limits and monitoring of resources.
</p>

### VM (Virtual Machine) vs. Containers
<p>
<ul>
  <li>Each VM has its own OS.</li>
  <li>VM is very heavy and slow to start.</li>
  <li>Containers shares the same base Kernel.</li>
  <li>Linux namespaces, not include the full OS.</li>
  <li>Quick to start due its lightweight feature.</li>
</ul>
Containers do not replace VMs. It is not one over other. Containers can work on the top of a VM. Containers often re-couple the infrastructure of an existing VM.
</p>

### What is Docker?
Dockers enables containers to be used by the masses. At its core, Docker is tooling to manage containers:
<li>Simplified existing technology to enable it for the masses.
</li>
Enable developers to use containers for their applications:
<li>Package dependencies with containers: <i>build once, run anywhere.</i></li>

### Why Containers are appealing to Users?
<ul>
  <li>No more <i>Works on my machine.</i></li>
  <li>Lightweight and fast.</li>
  <li>Better resource utilization</li>
  <ol>
    <li>Can fit far more containers than VMs into a host.</li>
  </ol>
</ul>
