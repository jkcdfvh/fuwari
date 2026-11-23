---
title: 如何正确开启UbuntuEdge源
published: 2026-11-22
description: 'Ubuntu AI 安全补丁来了：Edge 源是什么、值不值得开启'
image: ''
tags: [Linux, Ubuntu]
category: 'Linux'
draft: false 
lang: 'zh-CN'
---

# 前情提要
Ubuntu 系统以后可能要由 AI 来写安全补丁了，而且现在你就能自愿开这个口子。Canonical 已经正式上线了 Edge 源，一个可以让 Ubuntu Pro 用户提前拿到由 AI 生成，但还没走完全部人工质检的安全补丁的入口。那么，问题来了——AI 写的补丁，你真敢装吗？

Edge 源里面的补丁，全部出自 Canonical 自研的 Surge 框架，这是一套专门做「漏洞修复」和「回溯移植」的多智能体系统。它还给自己上了 3 道保险：

多模型竞争：同一个漏洞，会由多个相互竞争的模型各自生成候选补丁，不会去赌单个模型的输出。

评委共识：候选补丁会交给一组独立的「评委模型」打分，有分歧就做共识裁决。

人工兜底：低置信度、评委死锁和边缘情况，一律转交给 Ubuntu 安全工程师进行人工处理。

# 1. 启用前提

启用 Edge 仓库的前提，是你已经开通了 Ubuntu Pro（个人免费，最多 5 台设备），并且至少启用了 ESM Infra 或 ESM Apps 的其中一项。查看订阅状态： 

pro status

# 2. 配置 Edge 源


sudo apt install pro-edge
sudo pro-enable-edge

# 注:默认情况下，Edge 源的配置优先级要低于 Ubuntu 或 ESM 源，来自该源的更新不会自动安装，你手动挑补丁即可；想要自动更新，可以加参数：
sudo pro-enable-edge --automatic-updates

# Surge 智能体 + Edge 安全更新是 Canonical 在「AI 时代防守速度」上的一次探索：主打一个用 AI 修复去对冲 AI 漏洞挖掘，同时把「稳定」这条底线，留给了传统的人工质检通道。对 Ubuntu Pro 用户来说，它是一道可选的取舍题——要快，就开；要稳，就等正式补丁发布。我也不建议你在生产环境上盲目乱开。
