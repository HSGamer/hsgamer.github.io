---
title: "Not Work - Not Worth"
subtitle: "Don't say \"not work\". Please say details."
date: 2022-11-30T12:18:43+07:00
authors: ["HSGamer"]
description: "Don't say \"not work\". Please say details."

tags:
- not work
categories:
- development

comment:
  enable: true
share:
  enable: true
---

# Background

> You have a good day making progress on your public projects, then a stranger contacts you and tells you "your project doesn't work on my system" and no further details. What would you do?

This scenario has happened to me for a few times through my support channel. For the most part, I'd just tell the person to provide more details on the system they are using, how they set up my projects, the error they see, etc. Then wait for their response.

However, not just my services, others from my fellow developers and service providers usually occur the similar issue. Therefore, I made this post as a shortcut to teach the users on how to properly report their bugs.

# Don't

> _00:00_ - **User**: Hello. This feature doesn't work for me. How can I fix this?

> _05:00_ - **Support**: Hmmmm... Wierd, I didn't see the problem in my test system. Can you give me your config file on that feature?

> _06:00_ - **User**: Here is my config: config.yml

> _06:30_ - **Support**: You forgot to set `enabled` to `true`

> _07:00_ - **User**: Oh right, I forgot that. It works now. Thanks

The problem is that the **Support** might be either offline or "AFK" on the **User**'s first message, and it took `5 hours` for him to see that messages. However, he didn't know how the **User** had done to the project that caused the feature to `doesn't work`, so he guessed the **User** did something wrong in the config and asked the **User** to give him the file. Then, he had to wait for `1 more hour` to receive the needed file, just to see that the **User** didn't enable the feature. In summary, it took him `6 hours` only to get the necessary details to understand the **User**'s problem.

# Do

> _00:00_ - **User**: Hello. This feature doesn't work for me. How can I fix this?

> _00:30_ - **User**: Here is my config files: config.yml, features.yml, data.json

> _05:00_ - **Support**: You forgot to set `enabled` to `true` on your `config.yml`

> _06:00_ - **User**: Oh right, I forgot that. It works now. Thanks

Now it took the **Support** only `5 hours` to understand and give the **User** the possible solution. Time was not wasted.

# Alternative

There are some cases that the **User** doesn't know which files to give to the **Support**, because of how enormous the files are.

Here are possible solutions to ultimately solve the issue:

* **Provide all details**: Give all Config files, Logs, Stacktraces, Reports, Screenshots, Showcase, Demos, etc. Anything that is related to the project.
  * This might not be a good solution as the **User** has to provide sensitive information as parts of the details.
  * Because of security reasons, this is ultimately dangerous for projects / services that provide community support (forums, JIRA, fanpages, etc.). However, your project would be fine if it did not contain or store private data.
* **Bug template / Guideline**: Provide some kinds of forms / templates or Create a tutorial to teach the **User** how to report issues.
  * This is more common in big community projects.
  * The **Support** can specify which files the **User** has to provide. That means sensitive information can be avoidable.
  * The **Support** can also teach the **User** how to censor information in case parts of the private data is important for the investigation.

# Related

* [no hello](https://nohello.net/)
* [The XY Problem](https://xyproblem.info/)
* [Don't Ask To Ask](https://dontasktoask.com/)
