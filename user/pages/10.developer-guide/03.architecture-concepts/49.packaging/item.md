---
title: 'Packaging and Release Numbers'
---

<div class="notices blue"> We don't use version numbers, <a href="https://blog.corebos.org/blog/nomoreversions">it makes no sense in our project.</a>
</div>

Release Numbers
---------------

[Based on Producing Open Source Software](http://producingoss.com/en/development-cycle.html)

We will follow the convention laid out in the book [Produccing Open Source Software](http://producingoss.com) whereas, we will use three
number components in the version name:

&lt;wrap em&gt;major\_number.minor\_nomber.micro\_number&lt;/wrap&gt;

whereas:

1. Changes to the **micro number** only (that is, changes within the same minor line) must be both forward- and backward-compatible. That is, the changes should be bug fixes only, or very small enhancements to existing features. New features should not be introduced in a micro release.

2. Changes to the **minor number** (that is, within the same major line) must be backward-compatible, but not necessarily forward-compatible. It's normal to introduce new features in a minor release, but usually not too many new features at once.

3. Changes to the **major number** mark compatibility boundaries. A new major release can be forward- and backward-incompatible. A major release is expected to have new features, and may even have entire new feature sets.

Packaging
---------

There will only be one packaging system which is a compressed .zip
obtained from GitHub. We will create a list of milestone and official
version tags on this page.

We have decided to do that because (as can be seen in this whole
project) we believe that each part in the whole system must do their
work well, there is no sense in creating a wiki when dokuWiki is
exceptional, it is better to integrate dokuWiki and mantisBT together
than add that into the issue tracker. With that in mind, the effort to
create an automatic installable package is overkill when there are
projects that prepare exceptional WAMP stacks with all the problems
resolved and when Linux just gives it to you by default. All we need to
concentrate our efforts on is creating exceptional coreBOS
functionality.

Downloads
---------

In general the master branch will always be a stable version of the
product, we will be developing fixes and features in other branches and
only add the code to the master branch when we are satisfied with it's
stability, so you can always download the master branch for the latest
changes. That said, be careful as we you will have to patch the changes
to stable milestones yourself, we will only create migrations paths from
one milestone version to the next.

[The official list of milestones is here](../../../11.others/04.devel)
