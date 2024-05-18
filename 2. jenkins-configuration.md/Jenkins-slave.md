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
