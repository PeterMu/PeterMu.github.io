---
layout: post
title: jQuery中remove empty detach方法的区别 
description: remove 会把dom和绑定到dom上的事件和数据一起删除，empty和detach方法不会。 
category: tech
---
## empty()

- empty方法会删除它的子节点，同时也会删除文本域。
- 在子节点绑定的事件和数据不会删除。

##remove()

- remove方法会删除自己和所有子节点。
- 在自己和所有子节点绑定的事件和数据都会一并删除。

##detach()

- detach方法会删除自己和所有的子节点。
- 在自己和所有子节点上绑定的事件和数据不会删除。

> 当需要清楚节点，但是不需要清楚绑定的事件和数据，想要在后来的某个时刻需要重新加入时，使用detach或empty。
