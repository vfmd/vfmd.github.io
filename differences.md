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

 1. [Intra-word emphasis]: The original Markdown allows intra-word
    emphasis using Markdown emphasis constructs. vfmd doesn't.

 2. [Simplified reference link/image syntax]: The syntax description
    of the original Markdown does not talk about links like [this] as a
    short form of [this][]. vfmd encourages using links like [this]
    instead of like [this][].

 3. [Lists and the 4-space rule]: vfmd has a simpler and clearer rule
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
improvement that [John Gruber came up with][short-ref-syntax-gruber],
but this improved syntax isn't mentioned in his Markdown syntax
description page. Item #4 is the first problem that Jeff Atwood mentions
in his [Responsible Open Source Code Parenting] post.

[Three Markdown Gotchas]: http://blog.stackoverflow.com/2008/06/three-markdown-gotcha/
[short-ref-syntax-gruber]: http://six.pairlist.net/pipermail/markdown-discuss/2005-March/001117.html
[Responsible Open Source Code Parenting]: http://www.codinghorror.com/blog/2009/12/responsible-open-source-code-parenting.html

## Differences

<h3 id="intra-word-emphasis">Intra-word emphasis</h3>

[Intra-word emphasis]: #intra-word-emphasis

The original Markdown allows intra-word emphasis. For example, in the
original Markdown, the following:

    That is un*frigging*believable.

    That is un_frigging_believable.

will be converted to:

    <p>That is un<em>frigging</em>believable.</p>

    <p>That is un<em>frigging</em>believable.</p>

But actually, it's not _that_ uncommon to have literal underscores in
the middle of words, especially in filenames and URL fragments, so
interpreting them as indicators of emphasis would be incorrect and
confusing.

Moreover, intra-word emphasis results in ambiguity. For certain inputs
involving intra-word emphasis, there are multiple ways in which it can
be interpreted. For example:

    *One **Two Three***Four** Five*

The above input could mean any of the following HTML equivalents, and
the author of the text could have meant any of these with equal
probabilities:

  1. `<em>One <strong>Two Three***Four</strong> Five</em>`
  2. `<em>One <strong>Two Three</strong></em>Four** Five*`
  3. `*One **Two Three<em><strong>Four</strong> Five</em>`

The above example uses multiple words, but even if we allow only
intra-word emphasis that is contained within a word, the possibility of
ambiguous input still remains.

On the other hand, in Japanese (and maybe in some other languages as
well), there is no concept of using spaces to separate words. So,
disallowing intra-word emphasis results in problems like
[this][jap-md-1] and [this][jap-md-2]. So, in order to be able to use
any kind of Markdown emphasis construct in Japanese text, honouring
intra-word emphasis becomes necessary.

[jap-md-1]: http://six.pairlist.net/pipermail/markdown-discuss/2005-November/001723.html
[jap-md-2]: http://meta.japanese.stackexchange.com/questions/120/

Considering the above points, the cons of supporting intra-word emphasis
appear to outweigh the benefits. Therefore, it was decided that vfmd
would not allow intra-word emphasis.

In vfmd, it is not possible to emphasize only part of a word using vfmd
constructs. So, for an input vfmd that looks like this:

    That is un_frigging_believable.

the corresponding HTML output will be:

    <p>That is un_frigging_believable.</p>


<h3 id="simplified-ref-link-image-syntax">Simplified reference link/image syntax</h3>

[Simplified reference link/image syntax]: #simplified-ref-link-image-syntax

In vfmd, you are encouraged to specify reference links like this:

    Just ask [Google].

    [Google]: http://google.com/

The syntax page for the original Markdown doesn't mention this syntax,
but mentions the _implicit link name_ syntax, which looks like this:

    Just ask [Google][].

    [Google]: http://google.com/

Though the short form of the _implicit link name_ syntax (of using
[this] instead of [this[]) isn't mentioned in the syntax page for the
original Markdown, it was [conceived][short-ref-syntax-gruber] by John
Gruber himself and implemented in [Markdown.pl v1.0.2b2].

[short-ref-syntax-gruber]: http://six.pairlist.net/pipermail/markdown-discuss/2005-March/001117.html
[Markdown.pl v1.0.2b2]: http://six.pairlist.net/pipermail/markdown-discuss/2005-March/001125.html

Writing like [this] for links is a much cleaner link syntax than
[this][]. It really does make the text look not-marked-up. vfmd
encourages using links like [this] instead of like [this][], though it
supports both forms.


<h3 id="lists-and-4-space-rule">Lists and the 4-space rule</h3>

[Lists and the 4-space rule]: #lists-and-4-space-rule

The original Markdown syntax page suggests that blocks nested within
list items should be indented by 4 additional spaces.

On including paragraphs in list items, the original Markdown syntax page
says:

> List items may consist of multiple paragraphs. Each subsequent
> paragraph in a list item must be indented by either 4 spaces or one
> tab.

On including code blocks in list items, the original Markdown syntax
page says:

> To put a code block within a list item, the code block needs to be
> indented twice — 8 spaces or two tabs.

Though left unspecified, many implementations (including John Gruber's
Markdown.pl) extend this to nested lists as well, which results in some
rather unintuitive interpretation of lists.

For example, the input:

    - top
      - indented by two spaces
        - indented by four spaces
          - indented by six spaces
        - indented by four spaces

is interpreted according to the (implied) original Markdown syntax as:

<blockquote>
    <ul>
        <li>top
            <ul>
                <li>indented by two spaces</li>
                <li>indented by four spaces
                    <ul>
                        <li>indented by six spaces</li>
                    </ul>
                </li>
                <li>indented by four spaces</li>
            </ul>
        </li>
    </ul>
</blockquote>

vfmd redefines the syntax for nesting lists by requiring that nested
elements align vertically with the starting position of the first
paragraph of the list item.

For the above example, the vfmd interpretation would be:

<blockquote>
    <ul>
        <li>top
            <ul>
                <li>indented by two spaces
                    <ul>
                        <li>indented by four spaces
                            <ul>
                                <li>indented by six spaces</li>
                            </ul>
                        </li>
                        <li>indented by four spaces</li>
                    </ul>
                </li>
            </ul>
        </li>
    </ul>
</blockquote>

which follows the structure of the input text much more closely.

