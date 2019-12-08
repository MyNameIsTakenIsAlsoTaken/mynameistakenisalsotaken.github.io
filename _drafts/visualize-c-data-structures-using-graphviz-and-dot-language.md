---
excerpt_separator: "<!--more-->"
layout: post
title: Visualize C++ Data Structures using Graphviz and DOT language
tags:
- c++
- graphviz
enableNepali: false
feature-img: ''
thumbnail: ''

---
Generally, if you're working with a program that works with data, you'll use some data structure or another to conveniently work with it. Linked Lists, Trees, Graphs, Ropes, et cetera are all amazing tools which make working with data lot more fun.

I'm currently working on writing a compiler for my own programming language. And that entails, among many many other things, working on the AST, the Abstract Syntax Tree. The AST is basically a tree representation of a program. To make sure that my compiler is understanding the language that it's meant to compile, I often have to feed it some test program and inspect the generated AST.

<!--more-->

I wrote a compiler for my minor project in my 6<sup>th</sup> semester but the language it compiled to assembly was very basic. So back then, I got away with simply printing the tree 

Funnily enough, I spent less time writing code to actually generate the graph than I spent trying to make it look cooler. But given how much time I'm going to have to stare at and navigate these graphs, I think the time was worth it. 