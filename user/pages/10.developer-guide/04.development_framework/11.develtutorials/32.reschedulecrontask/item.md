---
title: 'How to dynamically reschedule a cron task'
metadata:
    description: 'How to dynamically reschedule a cron task'
    author: 'Joe Bordes'
content:
    items:
        - '@self.children'
    limit: 5
    order:
        by: date
        dir: desc
    pagination: true
    url_taxonomy_filters: true
taxonomy:
    category:
        - development 
        - cron
    tag:
        - howto
---

All cron tasks are executed inside the same context and with full access to the whole set of tasks to be launched. This has a few implications:

===

- you cannot "die" a cron script because it would effectively kill the whole set of cron tasks execution
  - as a corollary of the above you must also be VERY diligent with errors and exceptions making sure you catch them all and continue in a controlled manner
- you could, practically, pass information from one cron task to another using shared variables, but you must consider that the execution sequence of the tasks is defined by the administrator user in Settings &gt; Scheduled tasks and launch frequency varies as time goes by so your scripts may get out of sync. Idea: you could use [the message queue](../24.corebos_mqtm) or [settings service](../25.corebos_setting) to sync them.
- you have access to the Vtiger\_Cron object for your cron, so you could manipulate it

As an example of how to benefit from this way of working, let's see how you would go about rescheduling a cron task dynamically.

Let's suppose that you have a cron script that connects to some external service, collects some information and updates it in coreBOS. This script is set to launch daily at some time, but you know that the connection to the external service may fail and you don't want to wait another full day for the next sync to happen. The logic you want to implement is something like this:

- try to connect to external service
- if all goes well we execute script normally and set an error control variable to 0 (all good)
- if we could not connect
  - we reschedule the task to be launched in 1 hour
  - we mark the error control variable with 1 (as in "1 reschedule" done)
  - when the task is launched again we repeat the process
  - if we still cannot connect
  - we reschedule the task to be launched in 1 hour
  - we mark the error control variable with 2 (as in "2 reschedules" done)
  - when the task is launched again we repeat the process
  - this time we see that the error control variable indicates that this is the third time we try to connect with no success, so
  - we set the scheduled task to launch again tomorrow at the normal time
  - we set the error control variable to 0
  - we send an email to escalate and inform about the issue so manual operations can be taken

In order to implement the above logic, the first thing that we need is to be able to save the "state" of each execution in persistent storage so we can retrieve the number of unsuccessful connections and also reset the task to it's normal time when we are done.

We can use [coreBOS settings service](../25.corebos_setting) for this saving two variables.

The next thing we need is to understand how we can change the next time to launch for the task. For this, we need to understand [how the tasks are executed](https://github.com/tsolucio/corebos/blob/master/vtigercron.php#L58:L66).

- each task is instantiated in a **$cronTask** object variable
- then it is launched
- and finally it is marked as done:

```php
$cronTask->markFinished($cronTask->getdaily(), $cronTask->getLastStart());
```

Now, looking at how the **markFinished** method works, we can see that it adds the frequency to the last start date, so if we change the last start date before the increment is done we can define when we want our script to be launched again. In the case we are doing now we know that the **markFinished** method will increment the time with 24 hours, so if we want the script to be launched 1 hour from "now" then we have to set the last start time to 25 hours ago.

The code would look something like this:

```php
$connerror = coreBOS_Settings::getSetting('ExternalSyncConnectionError', 0);
$synctime = coreBOS_Settings::getSetting('ExternalSyncTime', '02:40'); // sync daily at 2:40 am

// try to connect

if (connection error) {
	if ($connerror>=2) { // reschedule to normal time and escalate
		coreBOS_Settings::setSetting('ExternalSyncConnectionError', 0);
		list($hour, $min) = explode(':', $synctime);
		$time=mktime($hour, $min, 0, date('m'), date('d')-1, date('y')); // yesterday at sync time so we add 24hours
		$cronTask->setLastStart($time);
		// send email
	} else { // reschedule in an hour
		coreBOS_Settings::setSetting('ExternalSyncConnectionError', $connerror+1);
		$time=mktime(date('h')+1, 0, 0, date('m'), date('d')-1, date('y')); // yesterday at sync time + 1 hour so we add 24hours
		$cronTask->setLastStart($time);
	}
} else {
	// do sync
	coreBOS_Settings::setSetting('ExternalSyncConnectionError', 0);
	list($hour, $min) = explode(':', $synctime);
	$time=mktime($hour, $min, 0, date('m'), date('d')-1, date('y')); // yesterday at sync time so we add 24hours
	$cronTask->setLastStart($time);
}
```

<div class="notices blue"> <a href="https://blog.corebos.org/blog/sendemail">Read here to learn how to send emails from inside coreBOS</a></div>

