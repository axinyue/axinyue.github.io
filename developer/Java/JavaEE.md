# Java EE

java ee 提供了企业级快速开发的规范和api合集。
划重点-快速-规范化。以及JavaEE API是否需要付费和依赖特定的付费包。规划是否在SE中同样延用。
POJO = Plain Java Object.
目前来说没有发现EE和SE在api和使用上有明显差别,我的SE版JDK同样包含EE上提到的api,看起来api是通用的。
针对收费问题，使用SE 1.8以后的更新将会收费。暂时不知道是否针对特性及使用上是否有印象，可以先1.8稳住。

通过对OpenJdk-15和JavaSE的一些对比，
在openJdk确实取消了javax.annotation.*包中的一些注解。针对JavaSE的企业收费看来不可避免了。
这里可以确定的是如果是使用了JavaSE某些特性，服务端的Open-JDK及运行环境极有可能导致某些依赖缺失。
OpenJDK和OpenJRE运行环境,应该在安装时包含两者,这里不确定，后续验证下运行时的环境选择。

## EE 分层应用架构
  分组件，构建可伸缩扩展的应用。

  - EE服务器以容器的形式为每个基础组件提供基础服务。
  - EE服务器提供了例如EJB容器的实现
  - EJB跨虚拟机远程调用？共享组件？RMI的实现？
  - EE xml web支持，通过xml实现简单的SOAP访问，基于XML 双向交互,这里不只简单的展示，还可用于服务之间的交互协议设定(如果足够简化)

## JavaSE 和JavaEE参考
https://docs.oracle.com/javase/tutorial/security/overview/index.html
https://docs.oracle.com/javaee/7/tutorial/index.html
https://docs.oracle.com/javaee/7/tutorial/overview007.htm

SE文档中所用到的反射,泛型这些语法特性都是比较使用的，其中RMI也适用于OpenJDK中


## ps.
* EJB 是否可以实现多虚拟机共享一个服务。
SOAP 简单对象访问协议