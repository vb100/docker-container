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
  <li>Open a terminal on your local computer and run this command: <code>docker container run -t ubuntu top</code><br>The docker run command first starts a <code>docker pull</code> to download the Ubuntu image onto your host. After it is downloaded, it will start the container.</br><code>top</code> is a Linux utility that prints the processes on a system and orders them by resource consumption. Notice that there is only a single process in this output: it is the top process itself. You don't see other processes from the host in this list because of the PID namespace isolation.</li><br>Containers use Linux namespaces to provide isolation of system resources from other containers or the host. The <code>PID</code> namespace provides isolation for process IDs. If you run <code>top</code> while inside the container, you will notice that it shows the processes within the <code>PID</code> namespace of the container, which is much different than what you can see if you ran <code>top</code> on the host.<br>Even though we are using the Ubuntu image, it is important to note that the container does not have its own kernel. It uses the kernel of the host and the Ubuntu image is used only to provide the file system and tools available on an Ubuntu system.</li>
  <li>Inspect the container: <code>docker container exec</code><br>This command allows you to enter a running container's namespaces with a new process.</li>
  <li>Open a new terminal. To open a new terminal connected to <i>node1</i> by using <a href="http://play-with-docker.com/">Play-with-Docker</a>, click <i>Add New Instance</i> on the left and then ssh from <i>node2</i> into <i>node1</i> by using the IP that is listed by <i>node1</i>.</li>
  <li>In the new terminal, get the ID of the running container that you just created: <code>docker container ls </code></li>
  <li>Use that container ID to run bash inside that container by using the docker container <code>exec</code> command. Because you are using bash and want to interact with this container from your terminal, use the <code>-it</code> flag to run using interactive mode while allocating a psuedo-terminal:<br><code>$ docker container exec -it b3ad2a23fab3 bash </code><br><code>root@b3ad2a23fab3:/#</code><br>You just used the docker container <code>exec</code> command to enter the container's namespaces with the bash process. Using docker container <code>exec</code> with bash is a common way to inspect a Docker container.</br><br>Notice the change in the prefix of your terminal, for example,  <code>root@b3ad2a23fab3:/</code>. This is an indication that you are running bash inside the container.
  <p><b>Tip</b>: <i>This is not the same as using ssh to a separate host or a VM. You don't need an ssh server to connect with a bash process. Remember that containers use kernel-level features to achieve isolation and that containers run on top of the kernel. Your container is just a group of processes running in isolation on the same host, and you can use the command docker container <code>exec</code> to enter that isolation with the bash process. After you run the command docker container <code>exec</code>, the group of processes running in isolation (in other words, the container) includes top and bash.</i></p>
  </li>
  <li>From the same terminal, inspect the running processes: <code>ps -ef</code>.<br>You should see only the top process, <code>bash</code> process, and your <code>ps</code> process.</li>
  <li>For comparison, exit the container and run <code>ps -ef</code> or <code>top</code> on the host. These commands will work on Linux or Mac. For Windows, you can inspect the running processes by using <code>tasklist</code>.<br>
<code>root@b3ad2a23fab3:/# exit</code><br>
  <code>exit</code><br>
  <code>$ ps -ef</code><br>
  <code># Lots of processes!</code><br>
  <p>PID is just one of the Linux namespaces that provides containers with isolation to system resources. Other Linux namespaces include:
  <ul>
    <li><code>MNT</code>: Mount and unmount directories without affecting other namespaces.</li>
    <li><code>NET</code>: Containers have their own network stack.</li>
    <li><code>IPC</code>: Isolated interprocess communication mechanisms such as message queues.</li>
    <li><code>User</code>: Isolated view of users on the system.</li>
    <li><code>UTC</code>: Set hostname and domain name per container.</li>
  </ul>
  </p>
  <p>
These namespaces provide the isolation for containers that allow them to run together securely and without conflict with other containers running on the same system.
</p>
</li>
<li>Clean up the container running the top processes:
  <code> < ctrl>-c</code></li>
</ol>

### Docker Images
<p><b>What is the Docker Image?</b><ul type='square'><li>TAR file containing a container's <b>filesystem</b> and <b>metadata</b>.</li></ul></p>
<p><b>The reason why we create Docker Images is?</b><ul type='square'><li>For <b>sharing</b> and <b>re-distribution</b>. Many containers can be created from a single Image. Images can be downloaded from the <a href="https://hub.docker.com/">Docker Hub</a> and then create a Docker container.</li>
  <li>To share Images we can use <b>Docker Registry</b>.<ul><li>Push and Pull Images from Registry</li><li>Default Registry: <b>Docker Hub:</b><ul><li>Public and free for public images</li><li>Many pre-packaged images available.</li></ul><li>Private Registry:</li><ul><li>Self-host or cloud prover options.</li></ul></li></ul></li></ul></p>
  
### Creating a Docker Image - with Docker build
<p>
<ol type="A">Create a <i>Dockerfile</i>:
  <ul>
    <li>List of instructions for how to construct the container.</li>
    <li><code>docker build -f Dockerfile</code></li>
  </ul>
</ol>
<br>
</p>
Example of <u>Ubuntu</u> Image.

~~~
Tildes are OK too.
~~~
