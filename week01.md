# Introduction to systems security

What is system? Elements that interact with each other. Why we need systems security and why it is important? Because systems are everywhere. Most systems contains multiple stacks, layers, languages, implementations, Oses, hardwares and all interacting together. Systems are also difficult to maintain, manage and integrate. Systems also mostly build in different times. Many systems have unknowns because of this. We call it legacy systems. Systems that is running but when something not right happens, it is very difficult to find out the problems. It is really fragile.

What is secure systems? It is system that can still achieve goals in the presence of an adversary. The security goal is to be able to implement security policy. E.g. CIA triads. When designing a secure system we want to talk about threat model. It is assumptions about adversary. There are two assumptions that we can make. Strong assumption and weak assumption. Strong assumption is when adversary can do something very specific and details. Weak assumption is when we define what adversary do based on general description. We want to define and provide mechanism to maintain security policy given the threat model. Some clear examples are provide authentication and do encryption. The success metric of secure system is when adversary within defined threat model can't violate the security policy.

It is difficult to build a secure systems. It is because security is a negative goals. In our side we want to protect all possible ways. But in the adversary side, they just need to find one way to attack. Adversaries just need to find the weakest link. We mentioned threat model which is assumption about adversary that will help to build a strong security policy. However, threat models in reality is hard. Often it is difficult to formalise. Another reason why systems security is difficult is because security is iterative process. Security is continous process. The thing that make more harms are, security often is not considered important by business and user requirement.

Next we will talk about Threat modelling. Again this is assumption about adversary. We will start with system model. Vulnerability is a defect with security consequences. Threat is potential danger to the system, usually targetting vulnerabilities. Attack is an attempt to damage or gain access to the system. Exploit is a successful attack. Trust boundary is where the level of trust change. We will talk again about trust later. Now we will go into more detail about threat modeling. What is the step to define assumption about adversary. First, we want to determine the attack surface for the application. Next, we will assign risk to the various threat. Last we want to drive the vulnerability mititgation process. TODO: research about how to assign risk!

There is a comic that describes accurately how threat modelling can go wrong. When one to crack and RSA encryption. It will need a very high computation power, even it is ever possible. But it can be simpler by threathening the person to decrypt the information, e.g by using a cheap wrench.

Now we will list several important security principles that can help to build  a secure systems. First is simplicity. It is clear. Simpler a design than less complicated and possible misinterpretations, wrong implementations or issues that can cause security issues.

Second open design. The clear examples is how all important encryption algorithms are open and public. That will help everyone to validate and find flaws and then fix it. Secret is difficult to protect. It will be easier to minimise the amount of secret.

Third, compartmentalization. The example is to create groups or roles. It is applied commonly in operating systems and information systems. However this can be complex. Example, groups are interact with each other. We need to think of how groups in different level can be interacted without elevating or downgrading security policies in the different level.

Fourth, Minimum exposure is to minimise attack surface. In API design we want to protect non public API behind proxy. Minimise windom of opportunity for adversary. E.g. cap login attempt. Slow it down with catcha.

Fifth, least privilege. Components or users of system should operate using the least set privilege necessary to complete the job. Strong example in unix is to never use root account. Least privilege help to minimise negative consequences of attacks and errors. However, this is not easy to implement.

Sixth, minimise trust and maximase trustworthyness. Why people trust? Why we trust when buying mineral water in supermarket? It is because it cheap to trust. It will cost you time and maybe money if you don't trust simple things that you do in daily life. Trust is good in society. But trust is not good in systems. We need to be curious and doubt. Trust is about something that need to be satiesfied. Trustworthy is when the expectation are satisfied.

Seventuh, secure and fail-safe defaults. System should start in and return to secure state in the event of failure. Interesting question. Should we default to unlock or to lock for secure door in the time of power failure? Is it better to have whitelist or blacklist access control? Whitelist might be better because we are allowing good defaults. While blacklist need the list to keep updated to block a new item that need to be blacklisted.

Eight, complete medation. Access to any object must be monitored and controlled. Access control must be operational during lifetime. Protection need to be made at the correct layer, usually alyer below attack. 

Nineth, no single point of failure. Build redundant mechanims whenever possible. SPOF might need to be implemented differently in the context of security and availability. In Secureity preventing SPOF is by diversing options. E.g by providing multi factor auth. But in availability, SPOF means to replciate or to clone.

Tenth, traceability. We have to log security-relevant system events. Keep log and confidential information. Some data might be required by law. And some data is also need to be stored securely.

There are few more principles such as generating secret which relate to maximizing the entropy of secret. The higher the entropy the more random the information. Some cases of how this principle is violated is the security questions to recover password. What is your mother name, city of birth and favorite color. The entropy of security question is really low. And it is very easy to narrow down. That is inscure. We also need to think about usability. E.g apps that disable pasting password is insecure because it prevent the user from using password manager.

Extra sample of security principle violations. Password recovery question as mentioned above. Time of check and time of use (TOCTTOU). TODO: undersatnd more how this can violate security policy. Buffer overlow and sql injections are other samples.

Next we will go to OS-level access, privileges, isolation and sandboxing.

First we will talk about privilege separation. How to limit potential bug? We want to divide system into modules. In unix there are users, processes, files, I/O, CPU and memory. We also build VM and nowadays containers. TODO: expaoin containers. Expalin diff between VM and containers. In network, there is also modularisation approach for privilege seperation. E.g network zone or VPC.

Next there is a very quick summary of unix privilege model. We start with principle which is a user. User is identified by uid and gid. It is defined in /etc/passwd, /etc/group and /etc/shadow. User also defines what privileges does process have. Subject is process with uid and gid. Object/process may act on files/directories, memory, other processes, I/O or IPC. TODO: make this into a blogpost.

In unix, users own directory. Users also own uid and gid. There is a special user with uid=0 that can do anything.

Files and directories have their own privileges. Files cann be read, write, exec and change permission. Files are asscoiated with uid and gid. Directoreis can be removed, linked, renamed or created. In unix file access is defined with rwx and for 3 different users/groups, started with owner, group and other. Examples: -rw-rw-r--. The file can be read and write by owner and group. But only can be read by others. Who can change file permission? It is only if file uid (owner) == user's uid or uid=0. There is a concept called filedescriptor that provides more granular access. TODO: blog about this too. The concept of fd is demonstrated in how sshd works. TODO: research about how sshd work and forking the process. Blog about this too.

In unix process can be created and killed. New process will get the same uid. To kill the process, user must have the same uid or uid=0. It is the same with debugging. One can change uid by calling system call setuid(new_id) (are you sure?). Only root uid=0 that can cahnge uid.

In unix networking a process can listen to a port. Port is logical network in transport layer of network (are yousure?). Only uid=0 can bind to ports < 1024. But anyone can connect to any port. One can only read/write to the owned socket. Root is required to send raw packets. TODO: what is sending raw packets? 

Some additional information. Setuid biunaries /biun/passwd is used to update /etc/passwd password. But how non root can update their password if /etc/passwd can be only updated by root? There is also security realted issues such as bugs and LD_PRELOADED. TODO: follow up this. In unix there is chroot command to change the root directory. TODO: for what is this is used? Docker will be on of it. Beside root, there is also needed a fine grained control. Last Unix by default using discretionary access control. Which mean the access control is defined by users. Alternative access control is mandatory access control that provides what to access in OS level. In Linux it is defined in SELinux. TODO: DAC vs MAC. Write also about SELinux.
