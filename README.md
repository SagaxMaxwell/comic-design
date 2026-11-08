---
date created: 2026-10-10T00:23
date updated: 2026-11-06T18:26
---

# 迷宫异世界设定

## 核心概念

没有等级面板或天生外挂。角色靠训练、实战、装备、知识与同伴关系成长。

核心命题：人在一次次选择中，成为能够使用力量的人。

## 设定目录

```base
filters:
  and:
    - 'file.inFolder("comic-design")'
    - '["md", "ipynb"].contains(file.ext)'
    - 'file.path != "comic-design/README.md"'
    - '!file.path.contains("/.")'
    - '!file.path.contains("/backups/")'
    - 'file.size > 0'
formulas:
  outline: |
    [
      ["world.md","世界观总纲"],
      ["growth.md","成长与技能"],
      ["equipment.md","装备与武器"],
      ["magic.md","魔法系统"],
      ["characters.md","角色设定"],
      ["story.md","剧情与创作原则"]
    ]
  position: 'formula.outline.reduce(if(file.path == "comic-design/" + value[0], index, acc), 999)'
  note: 'file.asLink(if(formula.position < formula.outline.length, formula.outline[formula.position][1], file.name))'
  topic: 'if(file.name == "world", "世界观", if(["growth", "equipment", "magic"].contains(file.name), "系统", if(file.name == "characters", "角色", if(file.name == "story", "创作", "其他"))))'
properties:
  formula.note:
    displayName: 笔记
views:
  - type: kanban
    name: 笔记
    groupBy:
      property: formula.topic
      direction: ASC
    groupOrder:
      - 世界观
      - 系统
      - 角色
      - 创作
      - 其他
    order:
      - formula.note
    sort:
      - property: formula.position
        direction: ASC
      - property: file.path
        direction: ASC
    columnWidth: 260
```
