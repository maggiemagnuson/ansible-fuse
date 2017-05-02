<h1>Jboss Fuse on Vagrant</h1>
<h3>Description:</h3>
<p>This install the JBoss Fuse server in Vagrant using Ansible.</p>

<h2>Requirements:</h2>
<ul>
<li>Ansible</li>
<li>Vagrant</li>
<li>VirtualBox</li>
</ul>

<h2>Steps to install and run</h2>
<h3>Clone GIT repository</h3>
<p>Choose the location where you want to clone the GIT repo.</p>
<pre>$ git clone git@git.target.com:z001hqv/ansible-vagrant-fuse.git</pre>

<h3><b>Download the JBoss Fuse .zip file into /roles/jboss-fuse-ensemble. You will need to do this from the JBoss Fuse website (http://www.jboss.org/products/fuse/download/). You will need to register with redhat in order to download it. You'll want to download version 6.1.0.GA. After it is downloaded and moved to /roles/jboss-fuse-ensemble, you want to RENAME the file to fuse-6.1.zip</b></h3>
<pre>$ mv downloaded_file_name fuse-6.1.zip</pre>

<h3>SSH to Vagrant VM</h3>
<pre>$ vagrant ssh</pre>

<h3>Change the dirctory to the fuse executable</h3>
<pre>$ cd /opt/fuse/bin</pre>

<h3>Start the JBoss Fuse server</h3>
<pre>$ sudo ./fuse</pre>

<h4>The JBoss Fuse server is now running. You'll see something like the following.<h4>
<pre>JBossFuse:karaf@root></pre>

<h3>Add an administrative user to the JBoss Fuse server</h3>
<pre>JBossFuse:karaf@root> esb:create-admin-user</pre>
<h4>Add administrative user</h4>
<pre>New user name: admin</pre>
<pre>Password for admin: admin</pre>
<pre>Verify password for admin: admin </pre>

<h3>Now the JBoss is ready to use. NOTE: You will need to keep this running in the state it's in or else the server will shutdown.<h3>

<h3>Launch the JBoss Fuse server console in your local browser</h3>
<pre>http://192.168.33.12:8181</pre>

<h2>Steps to install and run as a service - after JBoss Fuse has been installed</h2>

<h3>The Red Hat JBoss Fuse console's wrapper feature generates a wrapper around the JBoss Fuse runtime that allows you to install a message broker as a system service. The wrapper feature does not come preinstalled in the console, so before you can generate the service wrapper you must install the wrapper feature.</h3>

<h3>Once the feature is installed the console gains a wrapper:install command. Running this command generates a generic service wrapper in the JBoss Fuse installation.</h3>

<h4>To generate the service wrapper:</h4>
<h4>Start JBoss Fuse in console mode using the fuse command.</h4>
<pre>$ sudo ./opt/fuse/bin/fuse</pre>

<h4>Once the console is started and the command prompt appears, enter</h4>
<pre>JBossFuse:karaf@root> features:install wrapper</pre>

<h4>The features:install command will locate the required libraries to provision the wrapper feature and deploy it into the run time.
Generate the wrapper by entering</h4>
<pre>$ wrapper:install -n jboss-fuse -d jboss-fuse -D "service for JBoss Fuse"</pre>

<h3>On Redhat/Fedora/CentOS Systems:</h3>
  <h4>To install the service:</h4>
    <pre>$ ln -s /opt/fuse-6.1/jboss-fuse-6.1.0.redhat-379/bin/jboss-fuse-service /etc/init.d/</pre>
    <pre>$ chkconfig jboss-fuse-service --add</pre>

  <h4>To start the service when the machine is rebooted:</h4>
    <pre>$ chkconfig jboss-fuse-service on</pre>

  <h4>To disable starting the service when the machine is rebooted:</h4>
    <pre>$ chkconfig jboss-fuse-service off</pre>

  <h4>To start the service:</h4>
    <pre>$ service jboss-fuse-service start</pre>

  <h4>To stop the service:</h4>
    <pre>$ service jboss-fuse-service stop</pre>

  <h4>To uninstall the service :</h4>
    <pre>$ chkconfig jboss-fuse-service --del</pre>
    <pre>$ rm /etc/init.d/jboss-fuse-service</pre>
