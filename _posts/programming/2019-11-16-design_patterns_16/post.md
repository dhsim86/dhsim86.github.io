---
layout: post
title:  "디자인 패턴 16 - 중재자(Mediator)"
date:   2019-11-16
desc:  "디자인 패턴 16 -중재자(Mediator)"
keywords: "디자인 패턴, Design Patterns, 행동 패턴, 중재자, Mediator"
categories: [Programming]
tags: [Design Patterns]
icon: icon-html
---

중재자(Mediator) 패턴은 **객체 간의 상호작용을 캡슐화**하는 객체를 정의하는 패턴이다. 객체들이 서로 참조하지 않도록 하여 객체 사이의 소결합(loose coupling)을 촉진하며 **객체 간의 상호작용을 독립적으로 다양화시킬 수 있도록 한다.**

객체지향 개발 방법론에서는 행동을 여러 객체에 분산시켜 구현하도록 하여 **높은 응집성, 낮은 결합도**를 실현하도록 한다. 이러한 행동의 분산으로 각 객체는 객체의 재사용을 증대시킬 수는 있지만 **객체 구조는 수많은 연결 관계가 객체 사이에 존재하게 된다.**

이러한 **수많은 객체 간의 관계는 오히려 재사용성이 떨어질 수 있다.** 어떤 일 하나를 처리하기 위해서 수많은 객체가 개입되는 상호작용이 필요하게 되므로, 시스템의 행동을 변경하려면 수 많은 객체들을 한 번에 수정해야 되는 경우가 있다.

복잡한 연결 관계를 가지는 객체 집합에 대해서 **객체들 간의 상호작용과 관련된 행동을 하나의 객체로 모은 중재자 객체**를 둔다면 이러한 문제를 피해갈 수 있다. 중재자 객체는 상호 작용을 제어하고 조화를 이루는 역할을 하는데, **객체 집합에 속한 객체들의 참조자를 중재자 객체가 관리**하므로 **각 객체들은 다른 객체들에 대한 수많은 참조자를 가지는 대신 중재자 객체에 대한 참조자만 가지면 된다.**

> 객체 간의 의존성이 구조화되어 있지 않거나 잘 이해하기 어려울 때, 아니면 한 객체가 다른 객체를 너무 많이 참조하고 있고 너무 많은 의사소통으로 인해 그 객체를 재사용하기 힘들 때, 그리고 상황에 따라 객체들 간의 복잡한 상호작용 방법이 수정되어야 할 때 중재자 패턴을 사용할 수 있다.

![00.png](/static/assets/img/blog/programming/2019-11-16-design_patterns_16/00.png)

Mediator 객체는 **Colleague 객체와 교류하는데 필요한 인터페이스를 정의**한다. 이를 상속받는 ConcreteMediator 객체는 Colleague 객체와 조화를 이루어 상호 작용과 관계된 행동을 구현하며, 자신이 맡을 동료 객체(Colleague)들을 관리한다.

> 상호작용 방법이 변경된다면 Mediator를 상속받는 서브클래스를 하나 더 정의하여 반영하면 된다. 각 객체의 행동이 정의되어 있는 Colleague 객체는 변경할 필요없다.

Colleague 객체들은 **자신의 Mediator 객체를 참조자로 가지며**, 다른 객체(Colleague)와 상호 작용이 필요하면, 직접 호출하는 것이 아니라 Mediator를 통해 간접적으로 상호 작용한다. Colleague 객체들은 서로의 존재를 전혀 모르며, 단지 Mediator 객체만 알 뿐이다.

![01.png](/static/assets/img/blog/programming/2019-11-16-design_patterns_16/01.png)

어떤 일을 처리하는 데 있어서 개입되는 수 많은 객체들 사이에 Mediator 객체를 둠으로써 Colleague 객체들 사이의 종속성을 줄이고 객체 간의 협력 방법을 추상화시킬 수 있다. 

> 중재자 패턴은 서로 다른 객체들이 각자 책임에 맞게 잘 정의되어 있기는 하지만, 복잡합 상호작용 (한 객체가 다른 객체를 너무 많이 참조하거나 너무 많은 의사소통을 수행해서 재사용하기 어려울 때)을 가지거나 여러 객체에 분산된 행동이 상황에 맞게 한 번에 수정될 때 사용할 수 있다.

> 중재자 객체를 중간에 두어 객체 간의 다대다 연관관계를 일대다 관계로 만듬으로써 시스템의 복잡도를 완화할 수 있다. 하지만 중재자 객체에서 복잡한 상호작용과 관계된 코드를 구현하게 되므로 다른 어떤 객체보다도 복잡해질 수 있다.

> 중재자 객체와 행동을 담당하는 객체들끼리의 의사소통 구현은 감시자(Observer) 패턴을 활용할 수도 있다. 각 객체(Colleague)가 Subject 객체로 동작하여 상태의 변화가 일어날 때마다 중재자 객체에게 통보하면 중재자는 처리 방법에 따라 다른 객체들에게 변경을 통보하여 처리할 수 있다. 