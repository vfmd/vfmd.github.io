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

Moreover, there are several instances where the [vfmd syntax guide]
describes a syntax in a higher level of detail than the [original
Markdown syntax] guide. Those are not included as differences in this
document.

[Markdown]: http://daringfireball.net/projects/markdown/
[original Markdown syntax]: http://daringfireball.net/projects/markdown/syntax
[vfmd syntax]: http://vfmd.github.io/vfmd-spec/syntax/
[vfmd syntax guide]: http://vfmd.github.io/vfmd-spec/syntax/

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

 4. [Better automatic link detection]: In vfmd, straightforward links
    like `http://example.net` don't need to be surrounded in \<angle
    brackets\> to get automatically converted to links.

 5. [Double blank lines as end of blocks]: vfmd introduces a new rule
    that is not present in the original Markdown syntax, wherein two
    consecutive blank lines end the current blockquote or list or code
    block.

 6. [Starting number in lists]: vfmd honours the number you use to start
    a numbered list. In contrast, the original Markdown syntax always
    starts lists at the number "1", irrespective of what number is used
    to start the list in the source text.

 7. [Misnested constructs]: The vfmd specification defines how misnested
    constructs should be handled.  The original Markdown syntax does not
    document the behaviour on encountering such bad input. (To be fair,
    vfmd too doesn't include this in it's syntax guide page because most
    document authors don't need to know this).

 8. [Including raw HTML]: The original Markdown syntax page implies that
    HTML blocks can be freely included within Markdown, and shall be
    recognized correctly. In practice however, correctly figuring out
    where the HTML block ends is a hard problem for a Markdown parser,
    especially when there is no guarentee that the HTML shall be
    well-formed.

    vfmd sidesteps this problem by redefining how HTML should be mixed
    with Markdown. In doing that, it also optionally allows Markdown
    constructs to be used within HTML blocks.

None of these is new, really.

Items #1, #3 and #5 were the "gotchas" spotted by John Fraser as
discussed in [Three Markdown Gotchas]. Item #2 is a syntax improvement
that John Gruber and Aaron Swartz
[discussed][short-ref-gruber-aaron], but this improved syntax isn't
mentioned in the original Markdown syntax description page. Item #4 is
the first problem that Jeff Atwood mentions in his [Responsible Open
Source Code Parenting] post. Moreover, all these items have been
discussed multiple times in the [markdown-discuss mailing list].

[Three Markdown Gotchas]: http://blog.stackoverflow.com/2008/06/three-markdown-gotcha/
[short-ref-gruber-aaron]: http://six.pairlist.net/pipermail/markdown-discuss/2004-March/000303.html
[Responsible Open Source Code Parenting]: http://www.codinghorror.com/blog/2009/12/responsible-open-source-code-parenting.html
[markdown-discuss mailing list]: http://six.pairlist.net/pipermail/markdown-discuss/

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
original Markdown, it was [conceived][short-ref-gruber-aaron] by John
Gruber and Aaron Swartz, and implemented in [Markdown.pl v1.0.2b2].

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


<h3 id="better-auto-link-detection">Better automatic link detection</h3>

[Better automatic link detection]: #better-auto-link-detection

The original Markdown syntax requires that links be surrounded in
\<angle brackets\> for them to get linked up. For the input:

    Go to <http://example.net/> and find out.

the original Markdown syntax will produce the output:

    Go to <a href="http://example.net/">http://example.net/</a> and find out.

If the link is not surrounded in \<angle brackets\>, the original
Markdown syntax will not recognize that as a link.

So, for the input:

    Go to http://example.net/ and find out.

the original Markdown syntax will produce the output:

    Go to http://example.net/ and find out.

However, in plain text email (which is the inspiration for the original
Markdown and for vfmd), links are often found without the surrounding
\<angle brackets\>. Therefore, vfmd recognizes fully-formed links of the
form `scheme://path` even if they are not enclosed in \<angle
brackets\>.

For the input:

    Go to http://example.net/ and find out.

vfmd will produce the HTML output:

    Go to <a href="http://example.net/">http://example.net/</a> and find out.


<h3 id="double-blank-lines">Double blank lines as end of blocks</h3>

[Double blank lines as end of blocks]: #double-blank-lines

In vfmd, two consecutive blank lines signify the end of the current
block for blockquotes, lists and code blocks. This enables document
authors to write two blockquotes (or lists, or code blocks) one after
the other, without them getting merged into one blockquote (or list or
code block).

The original Markdown syntax does not specify such a rule.

For example:

<pre><code> 1. Item 1
 2. Item 2
 3. Item 3



    * Some other list
    * Some other list
</code></pre>

In vfmd, the above text will be interpreted as two separate lists,
rather than making the latter items a sublist of "Item 3". vfmd's
interpretation is more consistent with the structure of the input text.

This idea was [proposed][double-blanks-gruber] by John Gruber for
signifying the end of lists, but was never implemented in Markdown.pl.
vfmd adopts this idea for lists and extends it to blockquotes and code
blocks as well for consistency.

[double-blanks-gruber]: http://six.pairlist.net/pipermail/markdown-discuss/2006-October/000341.html


<h3 id="list-starting-number">Starting number in lists</h3>

[Starting number in lists]: #list-starting-number

In both vfmd and the original Markdown, the order of the numbers in a
numbered list is immaterial - the list will always be ordered correctly
in the output. In addition to that, vfmd allows the list to start at any
arbitrary number, while in the original Markdown, the list is always
assumed to start at the number "1".

The original Markdown syntax page says:

> If you do use lazy list numbering, however, you should still start the
> list with the number 1. At some point in the future, Markdown may
> support starting ordered lists at an arbitrary number.

vfmd honours the starting number used in the list and preserves that in
the output.

For example, vfmd would convert the following text:

    3. Cueball
    1. Black Hat
    1. White Hat
    7. Raptor

to the HTML output:

    <ol start="3">
        <li>Cueball</li>
        <li>Black Hat</li>
        <li>White Hat</li>
        <li>Raptor</li>
    </ol>

In contrast, the original Markdown will not include the `start="3"`
attribute in its output.

<h3 id="misnested-constructs">Misnested constructs</h3>

[Misnested constructs]: #misnested-constructs

Consider the input text:

    __strong *and__ em*

    [link text `and](url "with") code` span

The above are examples of misnested constructs. Whenever one span-level
construct appears intertwined with another span-level construct (instead
of one being nested within the other), the constructs are said to be
misnested.

The original Markdown syntax page does not define how these should be
handled, which is understandable, given that the original Markdown
syntax page is targeted at document writers.

In vfmd too, the handing of misnested constructs is not defined in the
syntax guide, but is defined in the specification page.

This is how vfmd handles misnested constructs:

 1. Code-spans and images take the highest precedence, with the
    first-occurring construct being prioritized

    For example, in ``[link text `and](url "with") code` span``, the
    code-span is identified, and the link is not honoured.

 2. HTML tags take the next precedence

    For example, in `__strong <i>and__ italics</i>`, the HTML tags are
    identified, but the strong emphasis is not honoured.

 3. All other span-level constructs together take the lowest precedence,
    with the first-occuring construct being prioritized.

    For example, in `__strong *and__ em*`, only the strong emphasis is
    honoured because it occurs first.

The idea that the first-occuring construct should be honoured was
[proposed][misnested-constructs-rus] by Jacob Rus and
[endorsed][misnested-constructs-gruber] by John Gruber.

[misnested-constructs-rus]: http://six.pairlist.net/pipermail/markdown-discuss/2006-September/000237.html
[misnested-constructs-gruber]: http://six.pairlist.net/pipermail/markdown-discuss/2006-September/000241.html


<h3 id="including-raw-html">Including raw HTML</h3>

[Including raw HTML]: #including-raw-html

The original Markdown syntax says this about including HTML blocks in
Markdown text:

> For any markup that is not covered by Markdown's syntax, you simply
> use HTML itself. There's no need to preface it or delimit it to
> indicate that you're switching from Markdown to HTML; you just use
> the tags.

> The only restrictions are that block-level HTML elements - e.g. `<div>`,
> `<table>`, `<pre>`, `<p>`, etc. - must be separated from surrounding
> content by blank lines, and the start and end tags of the block should
> not be indented with tabs or spaces. Markdown is smart enough not
> to add extra (unwanted) `<p>` tags around HTML block-level tags.

In practice, however, the identification of where the HTML block ends is
not consistent across implementations. In fact, it turns out that
identifying the end of the HTML block is quite a hard problem, if we
consider the possibility that the HTML block can have badly-formed HTML
(which is not quite an improbable scenario, actually).

If we know the end of the HTML block beforehand, it is possible to make
sense of badly-formed HTML containing misnested or unclosed tags. If
we're guaranteed that the HTML is well-formed, it is possible to
identify the end of the HTML block. But identifying the end of a
potentially badly-formed HTML block in a stream of text is an extremely
difficult (if not impossible) problem. Figuring out the end of the HTML
block is necessary to correctly process the rest of the input.

That apart, another point of concern is that sometimes, document authors
would like to have text within HTML blocks processed as Markdown (and
not as verbatim HTML). John Gruber [proposed][markdown=1 proposal] that
document authors add `markdown="1"` to the attributes of the block-level
HTML element within which Markdown is to be processed, like this:

    <div class="content" markdown="1">
    Markdown is processed *here*
    </div>

    <div class="summary">
    No Markdown processing here
    </div>


[markdown=1 proposal]: http://six.pairlist.net/pipermail/markdown-discuss/2004-August/000669.html
[Markdown.pl 1.0.2b4]: http://six.pairlist.net/pipermail/markdown-discuss/2005-September/001551.html

However, this solution fails to address the case where a verbatim HTML
block needs to be embedded within a Markdown-enabled HTML block.
For example, consider the case where our document is composed of a
hierarchy of block-level HTML elements, some of which need to be treated
as HTML blocks, and some of which need to support Markdown processing,
like this:

    *Abstract*: Some text here

    <div class="main-article">

    <div id="introduction">
        Intro text (needs Markdown processing)
    </div>

    <div id="content">
        Content text (needs Markdown processing)
        <div id="embedded-html-block">
            HTML block (no Markdown processing here)
        </div>
    </div>

    <div id="summary">
        Summary text (needs Markdown processing)
    </div>

    </div>

The `markdown="1"` solution does not address the above requirement.

Considering the above points, vfmd takes a different approach to
handling inline HTML. In vfmd, the Markdown-processable HTML blocks are
separated from the verbatim HTML blocks  with blank lines, like this:

    <div>

    Markdown processing done *here*

    <div>
    HTML block (no Markdown processing here)
    </div>

    Markdown processing done *here*

    </div>

In this approach, the verbatim HTML sections are visually separated from
the Markdown-processable sections, which makes the text comprehendible.
That said, this approach has been studied and
[dismissed][blank-line-to-separate-html] by John Gruber as being "too
arbitrary".

The vfmd approach also makes it unnecessary for an implementation to
figure out where a HTML block ends.

[blank-line-to-separate-html]: http://six.pairlist.net/pipermail/markdown-discuss/2004-March/000171.html

