---

layout: default  
title: "Differences with the original Markdown"  
permalink: differences/  

---

# Differences with the original Markdown

**vfmd** is a variant of [Markdown] with an unambiguous specification of
its syntax.

This document lists the differences between the [vfmd syntax] and John
Gruber's [original Markdown syntax].

Please note that in this document, the vfmd syntax is compared with the
syntax of the original Markdown as described in the [original Markdown
syntax] page, and not with Markdown.pl, which is an implementation of
that syntax.

[Markdown]: http://daringfireball.net/projects/markdown/
[original Markdown syntax]: http://daringfireball.net/projects/markdown/syntax
[vfmd syntax]: http://vfmd.github.io/vfmd-spec/userguide/

## Overview of the differences

In brief, these are the differences between the [vfmd syntax] and the
[original Markdown syntax]:

 1. **Intra-word emphasis**: The original Markdown allows intra-word
    emphasis using Markdown emphasis constructs. vfmd doesn't.

 2. **Simplified reference link/image syntax**: The syntax description
    of the original Markdown does not talk about links like [this] as a
    short form of [this][]. vfmd encourages using links like [this]
    instead of like [this][].

 3. **Lists and the 4-space rule**: vfmd has a simpler and clearer rule
    (in comparison to the original Markdown syntax) for nesting blocks
    inside lists, that results in more intuitive output for nested
    lists.

 4. **Better automatic link detection**: In vfmd, straightforward links
    like `http://example.net` don't need to be surrounded in \<angle
    brackets\> to get automatically converted to links.

 5. **Including raw HTML**: The original Markdown syntax page implies that
    HTML blocks can be freely included within Markdown, and shall be
    recognized correctly. In practice however, correctly figuring out
    where the HTML block ends is a hard problem for a Markdown parser,
    especially when there is no guarentee that the HTML shall be
    well-formed.

    vfmd sidesteps this problem by redefining how HTML should be mixed
    with Markdown. In doing that, it also optionally allows Markdown
    constructs to be used within HTML blocks.

None of these is new, really.

Items #1, #3 and (some aspects of) #5 were the "gotchas" spotted by John
Fraser as discussed in [Three Markdown Gotchas]. Item #2 is a syntax
improvement that [John Gruber came up with], but this improved syntax
isn't mentioned in his Markdown syntax description page. Item #4 is the
first problem that Jeff Atwood mentions in his [Responsible Open Source
Code Parenting] post.

[Three Markdown Gotchas]: http://blog.stackoverflow.com/2008/06/three-markdown-gotcha/
[John Gruber came up with]: http://six.pairlist.net/pipermail/markdown-discuss/2005-March/001117.html
[Responsible Open Source Code Parenting]: http://www.codinghorror.com/blog/2009/12/responsible-open-source-code-parenting.html
