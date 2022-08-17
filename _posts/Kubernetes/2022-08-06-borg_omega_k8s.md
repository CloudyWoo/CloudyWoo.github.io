

---
### Google의 integrated container management system
1. Borg
2. Omega
3. k8s

### Borg


### Omega

- Omega vs. k8s
	- comm
		- has at its core a shared persistent store
		  with components watching for changes to relevant objects
	- diff
		- Omega exposes the store directly 
		  to trusted control-plane components
		- Kubernetes is accessed exclusively through 
		  a domain-specific REST API that applies higher-level versioning,
		  validation, semantics, and policy

### k8s
Kubernetes was developed with a stronger focus on 
the experience of developers writing applications that run in a cluster: 
its main design goal is to make it easy to deploy and manage complex 
distributed systems, while still benefiting from the improved
utilization that containers enable.

---

### History of containers
#### early containers
1. via chroot : only provided isolation of the root file system
FreeBSD jail 

2. Solaris - cgroups
- Solaris subsequently pioneered and explored many enhancements
  particulary in Linux control groups(cgroups)


resource isolation by containers 
=> drive utilization much more higher than industy norm


#### modern containers
**it provides runtime isolation + image**

(Does image file represents minimization of dependecies?)

image file ? the file that makes up the application that runs inside the container

---
### Application-oriented infrastructure
benefits of container 
1. enables higher levels of utilization
2. Containerization transforms the data center from being
   machine oriented to application-oriented

#### Application environment
Q. What's the original purpose of the cgroup, chroot and namepace?
A. to protect applications from noisy, nosey, and messy neighbors.

Combining these with
container images created an abstraction that also isolates
applications from the (heterogeneous) operating systems on which they run.

decoupling if image and OS 
=> possible to provide the same deployment environment in
   both development and production
=> Improves deployment reliability and speeds up development by
   reducing inconsistencies and friction

#### How this abstraction works
(A)
having a hermetic container image that can encapsulate 
almost all of an application's dependencies into  a package
that can be deployed into the container.

(B)
If (A) is done correctly, the only local external dependencies 
will be on the linux kernel system-call interface

(+) improves portability dramatically
(-) can still be exposed to chrun in the OS interface
    particulary in the wide surface area exposed by 
    **socket options, /proc, and arguments to ioctl calls.**

-> so the goal of Open Container Initiative is
to clarify the surface area of the container abstraction.

-> container's worths were proven in Google
Google has only a small number of OS versions deployed 
across its entire fleet of machines at any one time

and it only needs a small staffs to maintain and update them.

#### How to achieve 'Hermetic' containers
1) Borg, program binaries are statically linked at build time
   to known-good library versions hosted in the company-wide repository
   
(problem) 
   Borg container image is not quite 'airtight' as it could have been
   Why? **applications share 'base image'** that is installed once 
   on the machine rather than being packaged in each container.

   the 'base image' containers utilities such as 'tar' and 'libc'
   베이스 이미지를 공유하기 때문에 베이스 이미지에 업데이트 등 변경사항이 발생하면
   실행 중인 모든 애플리케이션에 상당한 영향을 끼친다.

(solution)
2) Docker or ACI, 
   - harden the abstractions
   - get closer to hermetic ideal by eliminating implicit host OS dependencies
   - requiring an explicit user command to share image data between containers

#### Containers as the unit of management
Building management APIs around 'containers' vs. 'machines'

This thesis provides the 'primary key' of the data center's view
of machine to application switch.

#### Orchestration is the beginning, not the end

---
### Things to avoid
#### 1. Don't make the container system 'manage port numbers'
#### 2. Don't just 'number' containers: give them 'labels'
#### 3. Be careful with 'owmership'
#### 4. Don't expose raw state

---
### Some open, hard problems
#### 1. Configuration
- First, application configuration becomes the cathc-all location
  for implementing all of the things that the container management system doesn't do.
#### 2. Dependency management


---
### Conclusions



---
### 이해 잘 안 가는 단어/문장들

hermetic 
churn
airtight


(75) 
While this limited interface dramatically improves the portability of images






