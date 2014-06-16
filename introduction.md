---

layout: default  
title: "Introducing vfmd"  
permalink: introduction/  

---

# Introducing vfmd

**vfmd** is a variant of [Markdown] with an unambiguous specification of
its syntax.

vfmd stands for _vanilla-flavoured markdown_. It formalises [John
Gruber]'s [original Markdown syntax] as a fully-defined specification,
with some [modifications][differences] to the syntax.

[John Gruber]: http://daringfireball.net/
[Markdown]: http://daringfireball.net/projects/markdown/
[original Markdown syntax]: http://daringfireball.net/projects/markdown/syntax
[differences]: http://www.vfmd.org/differences/

<h2 id="background">Background</h2>

The [original Markdown syntax page] is really a syntax guide that helps
authors in writing a document in Markdown. For _implementers_ of
Markdown, the [original Markdown syntax page] is at best a set of
loosely defined guidelines on how an input shall be interpreted.
<span id="core-syntax">The syntax elements specified in the [original
Markdown syntax] constitute what is termed as the **core syntax** of
Markdown.</span>

Since the original Markdown was published in 2004, there have been many
different implementations of Markdown, written in different programming
languages, and many different flavours of Markdown, with additional or
modified features or syntax elements.  All these different
implementations and flavours of Markdown are based on the _core syntax_
as defined in the [original Markdown], but their interpretations have
[not always been consistent][babelmark2-faq], even when we consider just the
_core syntax_. This divergence implies that, unless written very
carefully to avoid any corner cases, a Markdown document is tied to the
variant of Markdown that was used while writing the document.

[original Markdown syntax page]: http://daringfireball.net/projects/markdown/syntax
[original Markdown]: http://daringfireball.net/projects/markdown/syntax
[babelmark2-faq]: http://johnmacfarlane.net/babelmark2/faq.html

Markdown would be a lot more valuable when different implementations and
flavours agree on the output for all input scenarios, atleast when using
just the _core syntax_.

One of the main reasons why the different variants of Markdown differ in
their behaviour is that there is no real specification for Markdown.  In
the absense of a specification, the developers behind the different
variants of Markdown have interpreted the loosely defined guidelines
specified in [original Markdown syntax] in different ways, thereby
resulting in this divergence.

A specification for Markdown would make it possible for different
implementations that adopt the specification to interpret an input in a
consistent manner.

<h2 id="prior-work">Prior work</h2>

There have been two significant attempts to unambiguously define the
Markdown syntax. Both include some syntax extensions, but neither of
them can be said to have comprehensively defined the _core syntax_ of
Markdown.

 1. **Markdown Extra Specification**

    [Michel Fortin], the creator of PHP Markdown, started work on a
    specification for the original Markdown plus the extensions in PHP
    Markdown. The [Markdown Extra Syntax specification] defines many
    block-level syntax constructs, but no span-level constructs are
    addressed as yet. The specification is not complete, and work on
    this seems to have [stopped as of July 2008].

 2. **Grammar from peg-markdown**

    [John MacFarlane]'s [peg-markdown] includes a [parsing expression
    grammar] for Markdown, which might be considered as a specification
    for Markdown. The included [PEG grammar file] contains both the
    grammar, and the code to be executed at specific points during
    parsing, and it appears that the grammar and the code are closely
    and inseparably integrated with each other.

    The grammar part of that file does not seem to be able to
    autonomously describe the Markdown syntax completely. For example,
    consider a bulleted list contained within a blockquote. The grammar
    does not describe this scenario by itself. Instead, the grammar
    specifies that blockquotes can contain arbitrary text. The
    implementation extracts the blockquoted arbitrary text and runs the
    parser on the extracted text to recognize block-elements within it.
    This is a perfectly acceptable design for an implementation, but
    this means that the grammar falls short of being able to represent
    the complete Markdown syntax independently.

[Michel Fortin]: http://michelf.ca/
[Markdown Extra Syntax specification]: http://michelf.ca/specs/markdown-extra/
[stopped as of July 2008]: http://thr3ads.net/markdown-discuss/2008/07/343649-standard-izing-extended-markdown#m343708

[John MacFarlane]: http://johnmacfarlane.net/
[peg-markdown]: https://github.com/jgm/peg-markdown
[parsing expression grammar]: http://en.wikipedia.org/wiki/Parsing_expression_grammar
[PEG grammar file]: https://raw.github.com/jgm/peg-markdown/master/markdown_parser.leg


<h2 id="design-of-vfmd">The design of vfmd</h2>

vfmd is designed with the following goals and guiding principles in
mind.

In adhering to these goals and principles, the vfmd syntax deviates in
some aspects from the [original Markdown syntax]. These [differences]
make it possible to define the syntax as a well-defined specification,
and also make the syntax a little more readable.

<h3 id="goals">Goals</h3>

The following are the goals for the vfmd specification:

 1. The vfmd specification shall unambiguously define the interpretation
    for all input scenarios for the _core syntax_ of Markdown
 2. Any input should be accepted as a valid vfmd document
 3. In case a vfmd implementation wants to support any additional syntax
    elements not covered by the _core syntax_ (e.g., fenced code-blocks,
    footnotes), the vfmd specification shall define how the handling of
    the custom additional syntax should be integrated with the handling
    of the _core syntax_

<h3 id="guiding-priciples">Guiding Principles</h3>

The following are the principles that guide the design of the vfmd
syntax, given in the order of their preference:

1. As far as possible, the vfmd syntax shall stick to the goal of the
   original Markdown: "Make it as readable as possible". Just like
   the original Markdown, the biggest source of inspiration for vfmd
   shall be the format of plain text email.
2. As far as possible, the vfmd syntax should make the input document
   follow the look and structure of the output richtext
3. As far as possible, the vfmd syntax shall not be different from the
   [original Markdown syntax]

[original Markdown syntax]: http://daringfireball.net/projects/markdown/syntax

<h2 id="thanks">Thanks</h2>

Many thanks to:

  * [John Gruber], who came up with the original Markdown syntax
  * [John MacFarlane], for [Babelmark2] and the [Babelmark2 FAQ] which
    were immensely useful in designing vfmd

[babelmark2]: http://johnmacfarlane.net/babelmark2/
[Babelmark2 FAQ]: http://johnmacfarlane.net/babelmark2/faq.html

<h2 id="contact">Contact</h2>

The vfmd project is by [Roopesh Chander].

Email: <roop@roopc.net>  
Twitter: [@roopeshchander](http://twitter.com/roopeshchander)

[Roopesh Chander]: http://roopc.net/
