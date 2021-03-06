---
layout: post
title:  "디자인 패턴 13 - 책임 연쇄(Chain of Responsibility)"
date:   2019-11-12
desc:  "디자인 패턴 13 - 책임 연쇄(Chain of Responsibility)"
keywords: "디자인 패턴, Design Patterns, 행동 패턴, 책임 연쇄, Chain of Responsibility"
categories: [Programming]
tags: [Design Patterns]
icon: icon-html
---

책임 연쇄(Chain of Responsibility) 패턴은 **요청을 보내는 객체와 이를 처리할 책임을 지는 객체들 간의 결합도를 없애기 위한 패턴이다.** 하나의 요청에 대해서 반드시 하나의 객체에서만 처리하도록 하지 않고, 여러 객체들에게 그 처리 기회를 주는 것이다.

이 패턴의 아이디어는 **처리를 요청하는 쪽과 처리를 담당하는 쪽을 분리**하는 것이다. 이를 위해 요청하는 쪽은 이 **요청을 처리할 객체를 명시하지 않으며**, 처리하는 쪽에서는 이 요청을 받아 이 요청을 처리할 적절한 객체를 찾을 때까지 어느 **객체 연결 고리를 따라 전달**한다.

> 어느 특정 요청을 처리하기 위해 처리할 객체를 명시하거나 하드코딩하는 것은 결합도를 높인다. 책임 연쇄 패턴은 처리를 요청하는 클라이언트와 이를 처리할 객체들을 분리한다.

객체 연결 고리를 따라 요청을 계속 전달할 수 있어야 하고, 요청을 처리할 객체를 명시할 수 없다는 것을 고려한다면, 모든 객체들은 **누구든지 동일한 요청을 받을 수 있어야 하므로 연결 고리에 존재하는 객체들은 동일한 인터페이스를 가져야 한다.**

![00.png](/static/assets/img/blog/programming/2019-11-12-design_patterns_13/00.png)

위와 같이 부모인 ChainHandler는 요청을 처리할 인터페이스를 정의하고, 후속 처리자(Successor)와 연결을 구현한다. 연결 고리에 연결된 그 다음 객체에 요청을 위임하도록 구현하면 된다. ChainHandler의 기본 처리 구현(handleRequest)은 자신에게 도달한 요청을 연결 고리에 정의된 다음 객체에 전달하도록 구현한다.

서브 클래스들은 특정 요청에 대해 처리할 수 있도록 구현하고, 만약 처리할 수 없다면 다음 객체에 위임하도록 구현한다.

전형적으로 객체 연결 고리는 다음과 같이 보일 수 있다.

![01.png](/static/assets/img/blog/programming/2019-11-12-design_patterns_13/01.png)

---

책임 연쇄 패턴은 다음과 같은 장점과 단점이 있다.

1. 객체 간의 행동적 결합도가 낮아진다.
    - 객체가 어떻게 요청을 처리하는지 몰라도 된다. 요청을 보내는 쪽에서는 이 요청이 적절히 처리될 것이라고 확신하기만 하면 된다.
    - 요청을 보내는 쪽이나 받는 쪽 모두 서로를 몰라도 되고, 연결 고리에 있는 객체들조차도 서로 어떻게 자신들이 연결되어 있는지 몰라도 된다. 자신과 연결된 그 다음 객체만 알면 된다.
2. 객체에게 책임을 할당하는 데 유연성을 높일 수 있다.
    - 요청을 처리할 책임을 여러 객체로 분산시킬 수 있고, 런타임에 객체 연결 고리에 요청을 처리할 객체를 추가, 제거함으로써 책임을 변경하거나 확장할 수 있다.
3. 처리가 항상 보장되지는 않는다.
    - 어느 특정 요청을 어느 객체가 처리할지를 명시하지는 않으므로, 요청이 처리된다는 보장이 없다. 만약 객체 연결 고리가 잘 정의되어 있지 않다면 해당 요청은 처리되지 못한채 버려질 수 있다.

[Chain Of Responsibility Example
](https://github.com/dhsim86/design_pattern_study/commit/03499d6027d7d4299eab1599c9d4b73119c895aa)