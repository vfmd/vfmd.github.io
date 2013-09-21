---

layout: default  
title: "vfmd: Markdown with a spec"  
permalink: /  

---

## What is it?

**vfmd** is a variant of John Gruber's [Markdown] with an unambiguous
specification of its syntax.

It's just plain-vanilla Markdown, but formalized with a spec. Hence
vfmd, or _vanilla-flavoured markdown_. (There are some differences with
the original Markdown, but arguably minor.)

For a more detailed introduction, see [Introducing vfmd].

## Why a spec?

Because the myriad implementations of Markdown don't quite agree on how
certain Markdown texts should be handled, which means that we never are
sure where our Markdown is going to work, and where not. For example, in
an ideal world, the Markdown we write using an app on my tablet should
work perfectly with a blogging engine, even though they use different
implementations of Markdown, created for different purposes and for
different platforms. An important reason why that's not the case now is
because Markdown has no spec - what exists, for the original Markdown,
and for the other variants, is a userguide that tells us how to write in
Markdown, not a spec that tells us unambiguously how Markdown should be
interpreted.

For more details on the motivation behind vfmd, see [Introducing vfmd].

## Does it have features 'foo' and 'bar'?

vfmd supports all syntax constructs in John Gruber's [Markdown], with
some differences. It does not define the syntax for the additional
features available in some variants of Markdown, like tables, definition
lists or footnotes.  However, extendability is part of the vfmd design,
so the specification includes information on how the syntax can be
extended to support features like that in an implementation of vfmd.

[Markdown]: http://daringfireball.net/projects/markdown/
[Introducing vfmd]: http://vfmd.github.io/introduction/

## What's up?

  * **Specification**:

    The [vfmd specification] is almost complete. This document describes
    the syntax for Markdown unambiguously and is intended for use in
    designing parsers for Markdown.

  * **Userguide**:

    The specification assumes basic knowledge of computer science
    concepts. For the convenience of authors, vfmd comes with a
    [userguide] which describes the syntax in detail, but to a much
    lesser degree than the specification. The userguide is work in
    progress.

  * **Tests**:

    A test suite is being developed to help in checking whether an
    implementation confirms to the vfmd syntax. The testsuite is work in
    progress.

  * **Implementation**:

    There are no implementations of vfmd yet. I plan to start work on an
    implementation after the userguide and testsuite are complete.

[vfmd specification]: http://vfmd.github.io/vfmd-spec/specification/
[userguide]: http://vfmd.github.io/vfmd-spec/userguide/

## How can you help?

Read up the spec. If you find any ambiguities, inconsistencies or stuff
that's just wrong, please open an issue (or pull-request) on the
[vfmd-spec repository].

[vfmd-spec repository]: https://github.com/vfmd/vfmd-spec/
