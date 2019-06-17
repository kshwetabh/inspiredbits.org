---
title: "How to Write Custom ESLint Rules for Your Project"
date: 2018-12-22T09:11:10+05:30
description: "Summary: This post explains how you can write custom ESLint rules for your project. The example included is a few custom rules for ExtJS framework based code."
tags: [eslint, tools, automation, javascript]
---

While researching for a better (I was using JSHint before) and customizable JavaScript Code linting tool, I found <a href="https://eslint.org" target="_blank">ESLint</a> and ever since have never looked back. ESList is modern, fast, customizable and cross-platform Node.js based static code analyser that looks for bad and problematic patterns in your JavaScript code.

Things that I love about ESLint tool:

- Blazing fast scanning provides immediate feedback
- Ability to add custom rules this is a huge win if you use a framework that is custom or is heavily customized.
- Node.js based and thus easier to install on other developer's workstation.
- How easy is to customize the rules and include other standard patterns in your project through its plugin feature (like SonarLint, etc.)

### When do you need to write a custom rule
Your project requires some custom rules that is very specific to your project annd is not covered by ESLint's standard set of rules (259 rules currently).

### Getting started with a custom rule

Writing your own rule involves the following steps:
1. 

<a href="/images/eslint-astexplorer.png" target="_blank"><img src="/images/eslint-astexplorer.png" alt="Eslint AstExplorer Image" class="responsive-post-image"/></a>


<div class="code">
{{< highlight javascript>}}
/*
 * Enforce using view.up() or view.down() methods instead of the expensive Ext.ComponentQuery.query() method 
*/
"no-hms-ext-componentquery": {
    create: function(context) {
        return {
            CallExpression(node) {
                if (node.callee && node.callee.object && 
                        node.callee.object.object &&
                        node.callee.object.object.type === "Identifier" && 
                        node.callee.object.object.name === "Ext" &&
                        node.callee.object.property && 
                        node.callee.object.property.type === "Identifier" &&
                        node.callee.object.property.name === "ComponentQuery" &&
                        node.callee.property && 
                        node.callee.property.type === "Identifier" &&
                        node.callee.property.name === "query") {
                    context.report(node, 'Avoid using Ext.ComponentQuery.query method, use view.down or popup.down method instead.');
                }
            }
        }
    }
}
{{< / highlight >}}
</div>   