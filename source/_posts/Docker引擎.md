---
title: Docker引擎
date: 2021-03-02 07:31:53
tags: docker
---

Dokcer引擎是用来运行和管理容器的核心组件。基于开放容器计划相关标准的要求，Docker引擎采用模块化的设计原则。当前Docker引擎是由Docker Client/Docker daemon/ containerd /runc组成。共同负责容器的创建和运行。

在发展过程中，为了更好的平台兼容性，使用Libcontainer代替LXC。摒弃大而全的daemon，拆开daemon功能分散到小的模块中。所有容器运行的代码都在一个单独的OCI兼容层中实现（runc）。

**runc**：run contianer ，实质上就是一个轻量级、针对Libcontainer进行包装的命令行交互工具。只有一个作用就是创建容器。

**containerd**：用来实现容器执行的所有逻辑，管理容器的生命周期，随后新增镜像管理的工作。

**shim**用来实现无daemon的容器的进程管理的工具。一旦容器创建完成，对应的runc进程就会退出，相关联的containerd-shim进程就会成为容器的父进程。

**daemon**的作用：主要包含镜像管理、镜像构建、REST API、身份验证、安全、核心网络以及编排。

通过将所有用于启动、管理容器的逻辑从daemon中删除，意味着与daemon与容器的解耦，可以被成为“无守护进程的容器”，因此对daemon的维护和升级不会影响到运行中的容器。





