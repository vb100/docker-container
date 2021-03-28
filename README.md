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
  <li>Each Vm has its own OS.</li>
  <li>VM is very heavy and slow to start.</li>
  <li>Containers shares the same base Kernel.</li>
  <li>Linux namespaces, not include the full OS.</li>
  <li>Quick to start due its lightweight feature.</li>
</ul>
Containers do not replace VMs. It is not one over other. Containers can work on the top of a VM. Containers often re-couple the infrastructure of an existing VM.
</p>
