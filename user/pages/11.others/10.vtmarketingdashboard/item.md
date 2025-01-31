---
title: 'vtMarketing Dashboard'
---

<div class="alert-danger">OBSOLETE</div>

[http://evolutivoteam.blogspot.com.es/2013/01/marketing-dashboard.html](http://evolutivoteam.blogspot.com.es/2013/01/marketing-dashboard.html)

**vtMarketing Dashboard** is a bundle of three vtiger CRM modules and an
advanced search and process extension which comes to fill the gap that
is missing between the campaign and the contacts.

![](emailmarketing.png?width=100%)

This set of extensions constructs upon the many to many relation
existent between contacts/leads and campaigns permitting us, not only to
massively fill a campaign but also create and track work being done upon
this relation.

With this tool we will be able to segment our market and associate each
segment with different campaigns, and then follow through on the emails
sent and the tasks being done on the campaign.

First we add a new module called **Message** where we can record every
interaction with the client and its outcome.

![](outcomes_of_email.png?width=100%)

This permits us to easily track the status of each email sent to the
contact, registering if the email was delivered, opened, bounced and
even if they clicked on any of the links in the email. We accomplish
full status information of our email campaigns from within vtiger CRM
with an easy to understand and use (standard) module.

Then we take this idea further and add a new **Task** module, which
emulates the existent vtiger CRM event/todo modules but following
standard module functionality, so we don't have to fight with the
restrictions and differences of the existing task module, making it also
very easy to implement enhancements on the work to be done both inside
vtiger CRM and outside (via REST).

![](creating_tasks_on_outcomes.png?width=100%)

Adding opportunities to the mix and creating a simple
**search-select-process** screen we give the user full control over the
campaign process.

![](potentials.png?width=100%)

The third module introduced is an email templating module which permits
the users to create their own templates for the campaigns.

Campaign Management
-------------------

In this tab, we will be able to **search-select-process** our campaigns.

In the first section of the extension, we find a set of different
options to segment our clients and prospects. We can **search** for
Leads, Contacts, Accounts, Messages, Tasks, and Potentials. In each of
these, we have different options to search upon. For example, the
contact section can be seen in the image below and it permits us to
search on a large combination of options like:

-   contacts related to a given account and/or campaign
-   contacts related to accounts contained in a filter
-   contacts contained in a filter and related to accounts contained in
    a filter
-   contacts with messages or tasks related to a campaign or not
-   ...

![](vtmkt_searchctos.png?width=100%)

In a similar manner, we can search in all the other entities.

Also, searches are accumulative, in the sense that for every search tab
which is left open, values will be looked up and mixed in the result
grid below, permitting an advanced combination of operations.

Once we have found the set of records we want to work with, we move on
to the next section where we are greeted with a grid containing all the
information we have found in our search. In this grid, we will be able
to filter further and **select** all the records which we really want to
work with.

![](vtmkt_selectctos.png?width=100%)

After selecting, we reach the **process** section of the extension. Here
we find four individual process tabs preceded by a set of general
parameters which affect all the process tabs.

![](vtmkt_processctos.png?width=100%)

The general parameters define the reference text, date, campaign and
user assigned to the new entities we will be creating in each process
section. For example, in the first **Message** section we will be able
to select an email template and massively send emails to all the
selected contacts. In the **Tasks** section, we would be able to program
calls or visits for the contacts and assign them a date and salesperson
as well as there initial status. We can also create business
**opportunities** to do the follow up of the campaigns and link back
into standard vtiger CRM features through the Opportunity module.
Finally, the last section will permit us to accomplish one of the most
demanded features in vtiger CRM forums: **massively link** many contacts
who have been filtered based on conditions from the account to a
campaign.

### Use Cases

Some typical use cases are:

-   **Campaign management**:
    -   segment market: create filters to segment our contacts, search
        for the contacts applying the filters and other restrictions,
        select all the contacts on the grid
    -   link to the campaign: open the Campaigns process tab and select
        the previously created campaign, link all the contacts to the
        campaign
    -   send emails: fill in the general parameters, especially the
        campaign so it gets related, open the message process tab and
        select a previously created email template, press the send
        button to create a message record for each contact and have an
        email sent for each message. As the user opens and reads the
        emails the status will be updated.

<div class="notices red"> For all those records that are
not even sent an email, because the email is empty or somehow wrong, it
will create a message record marked as <strong>"Not Sent"</strong>, so that we can
monitor the quality of our information easily using filters and/or
reports. </div>

      * create follow up tasks: after some time search for opened messages, select them and in the task process tab create tasks for the salespeople to call or visit the contact
      * for all those tasks with a positive response, create potentials which can be processed accordingly

Create Contacts
---------------

This tab permits us to create contacts from accounts. It is a mass
contact creator. The typical information from the account will be used.
The purpose of this functionality is to permit mass commercial efforts
working upon contacts exclusively. In certain situations where the
majority of our campaign will be done on contacts, having a certain
amount of accounts mixed with them is inconsistent. For these cases we
could create a contact for each account that does not have a contact
basically copying all relevant information from the account record. That
way we can launch campaigns working only with contacts.

Manage Assignments
------------------

In this tab we will be able to execute two processes:

-   **Mass related entity assignments**: With this functionality we will
    be able to work with comfort in those configurations where the
    information is private. When we work in a privately configured
    vtiger CRM and wish to assign an account or contact to another user,
    we find ourselves with the problem that we also have to change the
    assigned user to all the related entities of the account/contact,
    which quickly becomes a tedious task of many clicks and filters. The
    **mass assignments** process permits us to overcome the restriction
    and massively assign the account/contact and all its related
    entities to any user.

<!-- -->

-   **Copy values**: this process will permit us to copy the value of
    any field contained in a record to its related entities, which is
    very useful for workflows.

This tab follows the same **search-select-proces** method of the
previous tabs, but the work to be done will not be launched immediately.
Instead a cron task will be created and prepared to be launched when
programmed by the system administrator. A list of existing cron jobs can
be seen in the last **Cronjobs** tab, where we will also be able to see
the list of results of the last execution of any task. In the
**Cronjobs** tab we will also be able to manually launch a task or
eliminate it.

Unsubscribe from emails
-----------------------

The product is prepared to manage the case of clients who wish to
unsubscribe from the service and stop receiving emails.

We have two options to manage this.

If you have hired the service of sending emails with us (SendGrid), then
SendGrid is set to add an unsubscribe link in all emails. If someone
chooses this option they are automatically added to an exclusion list in
SendGrid which will not send them any further emails and this fact will
also be noted in the application, both in the message and on the record
of the lead, contact or account using the field "Do not send email "so
you can conveniently filter future mailings.

If you are in control of mailings with your own mail server, you must
add the link to your templates and prepare a landing page to inform the
user and launch a process to update your vtMarketing "Do not send email"
fields. Contact us if you need help.

FAQ
---

<div class="notices red">
<h2>I don't understand the sendgrid additional cost, I understand that
the extension includes control of emails sent (delivered, opened,
etc...)</h2>
<hr>

The Message module of the extension and the base vtiger CRM Emails
module has fields to control the state of the email sent, but this is a
manual process (as most things in vtiger CRM). If you want this to be an
automatic process we need to contract sendgrid service to do so, as they
will take care of the events and inform your vtiger CRM to update the
message and emails module. If your current email mass mail server can
handle these events also, contact us and we will help you get it
working. </div>
