---

layout: default  
title: "vfmd: Markdown with a spec"  
permalink: /  

---

## What is it?

**vfmd** is a variant of John Gruber's [Markdown] with an unambiguous
specification of its syntax.

It's just plain-vanilla Markdown, but formalized with a spec. Hence
vfmd, or _vanilla-flavoured markdown_. (There are some [differences]
with the original Markdown, but nothing big.)

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
and for the other variants, is a syntax guide that tells us how to write
in Markdown, not a spec that tells us unambiguously how Markdown should
be interpreted.

For more details on the motivation behind vfmd, see [Introducing vfmd].

## Does it have features 'foo' and 'bar'?

vfmd supports all syntax constructs in John Gruber's [Markdown], with
some [differences]. It does not define the syntax for the additional
features available in some variants of Markdown, like tables, definition
lists or footnotes.  However, extendability is part of the vfmd design,
so the specification includes information on how the syntax can be
extended to support features like that in an implementation of vfmd.

[Markdown]: http://daringfireball.net/projects/markdown/
[Introducing vfmd]: http://vfmd.github.io/introduction/
[differences]: http://vfmd.github.io/differences/

## Deliverables

The vfmd project aims to deliver the following:

  * **Specification**:
    A document describing the syntax for Markdown unambiguously and
    intended for use in designing parsers for Markdown.
    The specification document can be found [here][specification].

    _Status_: Done. However, it might undergo changes after
    testsuite-development / feedback.

  * **Syntax guide**:
    A document describing the syntax for Markdown, intended for use by
    document authors. This document needs to be consistent with the
    specification, and can have some ambiguities.
    The syntax guide can be found [here][syntax guide].

    _Status_: Done. However, it might undergo changes after
    testsuite-development / feedback.

  * **Tests**:
    A test suite to verify that an implementation confirms to the
    specification for HTML output. This needs to be consistent with the
    specification. The current set of testcases can be found
    [here][vfmd-tests-repo].

    _Status_: In progress.

  * **Implementation**:
    An implementation of the specification for converting vfmd text to
    HTML. The implementation should be extendable to support additional
    syntax elements in the way described in the specification.

    _Status_: Yet to start.

[specification]: http://vfmd.github.io/vfmd-spec/specification/
[syntax guide]: http://vfmd.github.io/vfmd-spec/syntax/
[vfmd-tests-repo]: https://github.com/vfmd/vfmd-tests

## How can you help?

Please take a look at the [specification], the [syntax guide] and the
[testsuite][vfmd-tests-repo]. If you find any errors, ambiguities or
inconsistencies, please submit an issue or pull-request in the
appropriate repository in [GitHub](http://github.com/vfmd).

If you have comments on the strategy or the core idea, please [contact
me](/introduction#contact).

