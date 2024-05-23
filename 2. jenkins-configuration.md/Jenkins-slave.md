## Jenkins Slave agent:

- The concept of a slave agent allows Jenkins to distribute its workload across multiple machines, enabling parallel and distributed builds.
  
- In Jenkins, the concept of "slave agents" (also known as build agents or nodes) is essential to distribute and parallelize build tasks across multiple machines. While the master node handles the Jenkins server's management and coordination, slave nodes allow for the concurrent execution of builds on different machines.

- Continuous build availability: If the master node becomes unavailable, builds can still be executed on slave agents.

-  You can configure different slave agents to specialize in particular tasks, such as building, testing, or deploying.

- Slave agents can run on machines with different operating systems or architectures. To handle a large number of builds concurrently and reduce build time.

## How to create the slave agent with SSH method: (java should installed on slave):

- follow below steps to launch the agent with SSH method.

```
Manage Jenkins – nodes – new node – permanent agent – create – name (Linux slave) – description (via SSH) – Number of executors (Number of concurrent builds the node can handle) –
remote root directory (home directory of user - /home/ec2-user) – labels (It helps specify where jobs can run based on labels) – launch method (launch agent via SSH) – host –
credentials (add SSH credentials with the username and private key) – host key verification strategy (manually trusted key verification strategy) – require manual verification of initial connection –
select  - require – save.

```


![image](https://github.com/gk-aws-dev/Jenkins/assets/154478305/560818e7-588d-4410-bebe-dc0e67f86108)

![image](https://github.com/gk-aws-dev/Jenkins/assets/154478305/e4370073-ef57-42e5-96f6-14b1cb7634a2)

-------------

## How to create the slave agent with JNLP method:

```
Manage Jenkins – name – permanent agent – remote root directory (/opt/Jenkins-jnlp – here we can run the agent.jar file)
– usage (use this node as much as possible) – launch method (launch agent) – availability – save.
```

- now open the port
```
Manage Jenkins – security - agent – TCP port for inbound agents – random (just need to select the port at random as we don’t know the port of the agent)
```

- Then click on the node – and download and run the agent file in the above root directory.
- we have to execute like the similar command (you can find the below command when you clicked on the slave)

```
curl -sO http://3.82.171.89:8080/jenkins/jnlpJars/agent.jar
java -jar agent.jar -url http://3.82.171.89:8080/jenkins/ -secret bd733e16c4f8edd247e9d4a4113b808d24ddd45ef9d41a006c6f03bc0385e045 -name "jnlp-new" -workDir "/opt/jenkins-jnlp"
```

(java should be install on the servers before giving above command)

then we must check the agent port and need to change it as fixed as below -> Manage Jenkins – security - agent – TCP port for inbound agents – fixed – port.

