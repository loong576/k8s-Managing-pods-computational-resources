k8s实践(六)：Pod资源管理

<br>

**环境说明：**

 
| 主机名 | 操作系统版本 | ip | docker version | kubelet version | 配置 | 备注 |
| :------: | :------:  | :------: | :------: | :------: | :------: |:------: |
| master | Centos 7.6.1810 | 172.27.9.131 |Docker 18.09.6 | V1.14.2 | 2C2G | 备注 |
| node01 | Centos 7.6.1810 | 172.27.9.135 |Docker 18.09.6 | V1.14.2 | 2C2G | 备注 |
| node02 | Centos 7.6.1810 | 172.27.9.136 |Docker 18.09.6 | V1.14.2 | 2C2G | 备注 |


<br>

&emsp;&emsp;在配置Pod时，我们可以为其中的每个容器指定需要使用的计算资源（CPU和内存）。计算资源的配置项分为两种：Requests和Limits。Requests表示容器希望被分配到的、可完全保证的资源量（资源请求量）；Limits是容器最多能使用的资源量的上限（资源限制量）。

<br>

&emsp;&emsp;资源请求量能够保证Pod有足够的资源来运行，资源限制量则是防止某个Pod无限制地使用资源，导致其他Pod崩溃,特别是在公有云场景，往往会有恶意软件通过抢占内存来攻击平台。

<br>

&emsp;&emsp;我们创建一个pod时，可以指定容器对CPU和内存的资源请求量及资源限制量，它们并不在pod里定义，而是针对每个容器单独指定。pod对资源的请求量和限制量是它所包含的所有容器的请求量和限制量之和。

<br>
<br>

**文章目录：**
# 一、计算资源管理（Compute Resources）
## 1. 概念
## 2. 查看节点资源总量
### 2.1 命令方式
### 2.2 Dashboard方式
## 3. requests
### 3.1 创建包含资源requests的pod
### 3.2 查看pod
### 3.3 基于requests的pod调度机制
#### 3.3.1 不指定requests
#### 3.3.2 OutOfmemory
#### 3.3.3 OutOfcpu
#### 3.3.4 结论
## 4. limits
### 4.1 创建包含资源limits的pod
### 4.2 limits overcommitted
#### 4.2.1 创建pod
#### 4.2.2 查看node01资源使用
#### 4.2.3 结论
# 二、服务质量管理（QoS）
## 1. 概念
## 2. 定义QoS
## 3. 相同等级QoS容器处理
# 三、资源配置范围管理（LimitRange）
## 1. 概念
## 2. 为什么需要LimitRange
## 3 创建LimitRange
## 4. 查看LimitRange
## 5. LimitRange测试
### 5.1 requests和limits默认值
### 5.2 强制限制
#### 5.2.1 cpu超限制
#### 5.2.2 内存超限制
# 四、资源配额管理（ResourceQuota）
## 1. 概念
## 2. ResourceQuota作用
## 3. 为CPU和内存创建ResourceQuota
### 3.1 查看ResourceQuota
### 3.2 resourcequota测试
## 4. 限制可创建对象的个数
### 4.1 查看ResourceQuota
### 4.2 resourcequota测试
## 5. 特定的pod状态或者QoS等级指定配额
### 5.1 查看ResourceQuota






<br>
<br>

**详细搭建过程及测试：**

https://blog.51cto.com/3241766/2428879
