## 概述

**原流程**：内容组与产品组都为 Master 的成员，都可以对 Master 进行推送操作。

![](https://main.qcloudimg.com/raw/2a845f6c064a200e8721e5fc24957c73.png)

**现流程**：内容组为 Master 的成员，产品组不属于 Master 的成员，产品组通过 Fork 操作，将拷贝了一份 Master 的副本，称为 Master Fork。产品组在修改文件之前需要手动进行同步操作，修改之后并 Push 在 Master Fork 后，需要发起【Pull Request】，由内容组审核。内容组审核通过后即可发布到 Master。

![](https://main.qcloudimg.com/raw/075be69601189b8ad10adff8b7687728.png)

## 特点

| 对比项 | 内容组 | 产品组 |
| --- | --- | --- |
| 克隆到本地 | 支持 | 支持 |
| Fetch Master | 支持 | 支持 |
| 修改本地文件 | 支持 | 支持 |
| 保存修改记录到 Git | 支持 | 支持 |
| 推送修改记录到 Master | 支持 | **不支持** |
| 发送 Pull Request | 支持 | 支持 |
| 处理冲突 | 支持 | 支持 |

## 产品组操作

### Fork 项目

产品组不属于项目的成员，需要将项目标记为 Fork，获取一个副本。

![](https://main.qcloudimg.com/raw/88b29400a41fc2943e9f46114344302d.png)

### 下载项目

点击 Fork 后，GitHub 为产品组自动创建一个副本。单击【Clone or download】。单击【Open in Desktop】。

> **注意**：
> - 必须确认下载的版本时，右上角为产品组个人 ID。若不是，请先 Fork 项目。
> - 如果不能直接打开 GitHub Desktop，也可以手动复制链接到 GitHub Desktop 进行添加。

![](https://main.qcloudimg.com/raw/9343a125457e7d82f5808fc312d8c3f7.png)

### 同步项目

Fork 后，产品组的版本将**不再自动与内容组的版本同步**，在修改文件前需要进行手动同步，尽最大可能减少冲突。若产品组每次修改本地文件前都不进行同步，那么最终可能产生大量的冲突。

单击【Branch】。单击【Merge into current branch】。

![](https://main.qcloudimg.com/raw/26c66ed25cad0d0aa225c19ca333e5f8.png)

单击【upstream/master】。单击【Merge into Master】。

>注：此处父项目（内容组负责的项目）为【upstream/master】，根据实际情况选择父项目的名称。

![](https://main.qcloudimg.com/raw/75898245bb548978f0530eb0e6d23f02.png)

### 修改本地文件

在本地修改文件，【Commit to Master】并【Push origin】。

>注：修改的记录会保存到产品组个人的副本中，不会推送至内容组负责人下的 Master。

![](https://main.qcloudimg.com/raw/b0ceaa51e5db2cfe1964813ba38a911e.png)

### 发送 Pull Request

单击【Branch】，单击【Create pull request】。

![](https://main.qcloudimg.com/raw/6a67e9a99d5a0428ad89e70214718a5b.png)

确认修改的信息是否正确，单击【Create pull request】。填写 comment，并单击【Create pull request】。

![](https://main.qcloudimg.com/raw/f1daaec9618ab39e8323cf447a5be007.png)

### 通知内容组更新

产品组需要将上一步的【Pull Request 链接】发送组内容组相关成员进行审核。

## 内容组操作

### 查看更新内容

打开【Pull Request 链接】，单击【comment 信息】可以查看产品组修改的文件。

>注：若网页不方便查看，也可以单击【open this in GitHub Desktop】，在 GitHub Desktop 单击【History】进行查看。

![](https://main.qcloudimg.com/raw/ab05e2597d1401836c7f2f3d15343972.png)

### 处理 Pull Request

确认信息无误后，单击【Merge pull request】。填写 comment 并单击【Comfirm merge】。

>注：也可以通过 GitHub Desktop 进行【merge】来处理 Pull Request。但网页处理更直观简便，出错率低。

![](https://main.qcloudimg.com/raw/4e1db731605f9a48dedc8f8e2f258a48.png)

## 冲突操作

### 冲突的产生

冲突产生的根本原因是**同一文件的同一个位置被同时修改**。由于 Git 在每一个 Push 后会生成一个节点，因此此处的【同时】指同一个 Push 的时间节点。**在每次修改文件前进行【同步】操作可以减少冲突**。以下分析两种冲突产生的典型案例：
- **案例 1**：产品组修改了文件，暂未【Pull Request】，但内容组修改了同一文件的同一位置，产品组此时【Pull Request】则提示有冲突。
- **案例 2**：内容组修改了文件，已经 Push 到 Master，但产品组修改了同一文件的同一位置，产品组此时【Pull Request】则提示有冲突。

### 冲突处理

**案例 1**：

产品组将【Boy】修改为【Cat】并 commit，但未【Pull Request】。

![](https://main.qcloudimg.com/raw/01b59b7363ef904f2d4034c6b506a5ad.png)

产品组修改的内容并未提交，故内容组不知情。此时内容组将【Boy】修改为【Dog】。

![](https://main.qcloudimg.com/raw/14ab783391e494c31ad20caf4d6841ad.png)

产品组将修改【Pull Request】后，提示有冲突。

![](https://main.qcloudimg.com/raw/5c1b923f9b1679972a6fe48b26a2dad8.png)

**案例 1 解决方案**：产品组处理冲突、内容组处理冲突，两种方式任选一种即可解决。

**产品组处理冲突**：

产品组在【Pull Request】时，能够第一时间发现冲突。此时产品组执行【同步项目】，即可查看冲突，根据实际情况重新编辑文件，解决冲突。

> - 【<<<<<<< HEAD】与【=======】之间为本地版本。
> - 【=======】与【upstream/master】之间为 Master 的版本。
> - 具体以哪个为准，需要修改的双方相互确认。确认后，删除相应的行，commit 并 Push 即可。

![](https://main.qcloudimg.com/raw/3ec10246087c4fc85cf4827c692c11af.png)

重新【Pull Request】后，发现并无冲突。

![](https://main.qcloudimg.com/raw/8f1617187d3a67b464853b52919e100b.png)

**内容组处理冲突**：

产品组在【Pull Request】时发现冲突，可以选择不理会，直接向内容组发送【Pull Request】。

![](https://main.qcloudimg.com/raw/72d024136dd9b64097bf7f5ff4bb73f8.png)

内容组收到产品组的【Pull Request】，提示有冲突需要处理，点击【Resolve conflicts】在网页端处理冲突。

>注：点击【open this in GitHub Desktop】可以在 GitHub Desktop 中处理。但需要在 GitHub Desktop 中手动 merge 分支。

![](https://main.qcloudimg.com/raw/df04723fbeab96c365f73cb4dfb2d826.png)

根据实际情况删除冲突的行，单击【Mark as resolved】。

![](https://main.qcloudimg.com/raw/7c6147da4aded9ab61f03a66be16bbfd.png)

再单击【Commit merge】，系统提示冲突解决。

单击【Merge pull request】即可。

![](https://main.qcloudimg.com/raw/e94381b0e00f93d1247bec6be74b18d8.png)

**案例 2**：

案例 2 的冲突处理方案与案例 1 相同。

## 优缺点

**优点**：

- 权限管理更加明确，可以防止产品组的误操作。

**缺点**：

- 流程变长。
- 产品组需要学习【Fork】、【同步】、【Pull Request】三个操作。
- 任何人都可以【Pull Request】，需要由内容组成员人工判断。
