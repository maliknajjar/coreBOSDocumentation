---
title: 'Separate RelatedTo field on Potentials'
---

Separate RelatedTo field on Potentials
======================================

This enhancement, which is coreBOS Updater compatible and does not
modify any base files, will separate the Account/Contact RelatedTo field
on the Potentials module.

The current field will be used for Accounts, so all records that are
related to accounts stay the same. If the Potential is related to a
Contact, the current value in the RelatedTo field will be copied to the
new Contact field and the RelatedTo field will get filled in with the
Account related to the selected Contact.

&lt;WRAP center round alert 80%&gt; This change can **NOT** be undone.
Once the changeset has been applied we must work with both fields
separated. &lt;/WRAP&gt;

---- dataentry ---- name : PotentialSeparateRelatedTo type : enhancement
description\_wiki: This enhancement will separate the Account/Contact
RelatedTo field on the Potentials module. keywords\_tags : Potentials,
RelatedTo, separate, Account, Contact version : 1.0 homepage\_url :
<http://corebos.org/documentation/doku.php?id=en:extensions:extensions:enhancepotrelto>
release\_dt : 2015-05-20 license : Vizsage price: 55eur buyemail\_mail:
paypal(at)tsolucio(dot)com distribution: Sale authorname : JPL TSolucio,
S.L. authoremail\_mail :info(at)tsolucio(dot)com authorhomepage\_url :
<http://tsolucio.com> supportemail\_mail :info(at)tsolucio(dot)com

------------------------------------------------------------------------