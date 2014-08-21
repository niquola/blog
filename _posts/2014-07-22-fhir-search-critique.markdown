---
layout: post
title:  "FHIR Search implementation notes"
date:   2014-07-22 12:00:00
abstract: Implementation notes & critique of FHIR search
categories: FHIR HealthIT
---


## REST & hypermedia

The essence of REST is described in [Roy Fielding dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm).

The *hypermedia* concept is clarified in his post [REST APIs must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
and comments to this post.


Here is critique of OpenSocial REST API by Roy Fielding:

> The OpenSocial RESTful protocol is not RESTful.
It could be made so with some relatively small changes,
but right now it is just wrapping RPC results in common Web media types.

> A truly RESTful API looks like hypertext.
Every addressable unit of information carries an address,
either explicitly (e.g., link and id attributes) or implicitly
(e.g., derived from the media type definition and representation structure).
Query results are represented by a list of links with summary information,
not by arrays of object representations (query is not a substitute for identification of resources).
Resource representations are self-descriptive:
the client does not need to know if a resource is OpenSocialist
because it is just acting on the representations received.

> Think of it in terms of the Web. How many Web browsers are aware of the distinction
between an online-banking resource and a Wiki resource? None of them.
They don’t need to be aware of the resource types. What they need to be aware
of is the potential state transitions — the links and forms — and what semantics/actions are implied by traversing those links. A browser represents them as distinct UI controls so that a user can see potential transitions and anticipate the effect of chosen actions. A spider can follow them to the extent that the relationships are known to be safe. Typed relations, specific media types, and action-specific elements provide the guidance needed for automated agents.

Looks like FHIR specification is making same mistake.
Design FHIR media type with hypermedia controls allows
to implement more generic, extendable and reliable clients.


## FHIR Search API: Modifiers & Value Prefixes

FHIR specification describes [modifiers](http://www.hl7.org/implement/standards/fhir/search.html#modifiers)
& value prefixes (http://www.hl7.org/implement/standards/fhir/search.html#number).

They are almost orthogonal (i.e. never used together) except :missing modifier.

There is one problem with modifiers:

Most popular web frameworks & libs tend to treat query params as hash-map or dictionary.
Modifier breaks this mapping by changing key signature and bring some extra complexity to implementation.

```
a=b&c=d => {"a": "b", "c": "d"}

a:mod=b&c=d => ?
a:mod=1&a=2 => ?
```

Query params are used to encode search predicates.
Predicates are traditionally expressed
with infix binary or unary operators (like in SQL standard):

```
[left]  [op]      [right]

name    like      '%nicola%'
age     >         200
fact    is null
```

The point is replace modifiers with value prefixes (operators).
This simplify design and make query string more like hash-map (dictionary).

Here is possible ways of modifier removal:

```
parameter={op}value

# move modifier to value
_sort:asc=a&_sort:desc=b => _sort=name|asc,date|desc

name=nicola          => name={like}nicola or name=%nicola
name:exact           => name={exact}nicola or name==nicola

gender:text          => gender={text}male

# unary operators
gender:missing=true  => gender={null} or gender={empty}
gender:missing=false => gender={notnull} or gender={present}

# move resource type to value
subject:Patient=123  => subject=Patient|123
```
