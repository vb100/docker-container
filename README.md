## Docker. Explained.

This Readme file provides the main key points about the what the Dockers are and how they can be used in MlOPS, DevOps, and in Data science.

### What are Containers?
<p>A group of processes run on isolation.
<ul type="square">
  <li>All processes must be able to run on the shared kernel.</li>
</ul></p>

<p>Each container has its own set of <b>namespaces</b> (<i>isolated view</i>):
<ul type="square">
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
<ul type="square">
  <li>Each VM has its own OS.</li>
  <li>VM is very heavy and slow to start.</li>
  <li>Containers shares the same base Kernel.</li>
  <li>Linux namespaces, not include the full OS.</li>
  <li>Quick to start due its lightweight feature.</li>
</ul>
Containers do not replace VMs. It is not one over other. Containers can work on the top of a VM. Containers often re-couple the infrastructure of an existing VM.
</p>

### What is Docker?
<ul type="square">
<li>Dockers enables containers to be used by the masses. At its core, Docker is tooling to manage containers:</li>
<ol type="A">
  <li>Simplified existing technology to enable it for the masses.</li>
</ol>
  <li>Enable developers to use containers for their applications:</li>
<ol type="A">
  <li>Package dependencies with containers: <i>build once, run anywhere.</i></li></ol>
</ul>

### Why Containers are appealing to Users?
<ul type="square">
  <li>No more <i>Works on my machine.</i></li>
  <li>Lightweight and fast.</li>
  <li>Better resource utilization</li>
  <ol type="A">
    <li>Can fit far more containers than VMs into a host. You can run many containers on the same infrastructure without conflicts and save a lot of money.</li>
  </ol>
  <li>Standard developer to operations interface.</li>
  <li>Ecosystem and tooling.</li>
</ul>

<p>
  <b>Useful links:</b>
  <ul type="square">
    <li><a href="https://docs.docker.com/">Full Docker Docummentation (Official)</a></li>
    <li><a href="http://play-with-docker.com/">Play-with-Docker</a></li>
</ul>
</p>

## Hands-on practice
### Run first container

<p>Use the Docker CLI to run your first container.</p>
<ol type="A">
  <li>Open a terminal on your local computer and run this command: <code>docker container run -t ubuntu top</code><br>The docker run command first starts a <code>docker pull</code> to download the Ubuntu image onto your host. After it is downloaded, it will start the container.</br><code>top</code> is a Linux utility that prints the processes on a system and orders them by resource consumption. Notice that there is only a single process in this output: it is the top process itself. You don't see other processes from the host in this list because of the PID namespace isolation.</li><br>Containers use Linux namespaces to provide isolation of system resources from other containers or the host. The <code>PID</code> namespace provides isolation for process IDs. If you run <code>top</code> while inside the container, you will notice that it shows the processes within the <code>PID</code> namespace of the container, which is much different than what you can see if you ran <code>top</code> on the host.<br>Even though we are using the Ubuntu image, it is important to note that the container does not have its own kernel. It uses the kernel of the host and the Ubuntu image is used only to provide the file system and tools available on an Ubuntu system.
</ol>
