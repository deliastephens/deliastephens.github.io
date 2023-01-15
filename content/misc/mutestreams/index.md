---
title: MuteStreams
dateMonthYear: August 2016
description: Automatic muting for annoying commercials.
image: /images/mutestreams.PNG
---

In middle school, I had an idea: what if your TV could be muted automatically? While there existed programs to evaluate changes in television volume and search closed captioning devices for "trigger words", no robust, easy-to-use system existed to mute a television automatically. Thus, MuteStreams was born.

For my invention, I was awarded two U.S. Patents: [Methods for Processing Mute Signals](https://patents.justia.com/patent/9357259) and [Systems and Methods for Controlling Broadcast Audio Volume](https://patents.justia.com/patent/9210466).

The invention was an easy way for "subscribers" to have their televisions automatically muted by more vigilant users. These vigilant users would mute their televisions when a commercial came on. This "mute signal", interpreted by a device plugged into the set-top box and comprised of the mute instance and a program number, would be sent by TCP/IP protocol to a remote server, aggregated with other mute signals, and distributed across a network to the subscribers.

The project included many technical challenges: how are mute signals distributed? What makes a signal "good"? What happens when someone just mutes their TV to have a conversation with a friend? We had to examine every contingency in order to get an idea that would theoretically work. The project required hours of discussion and iteration.

In this way, subscribers could have their televisions automatically muted. Central to this invention was the concept of "mute credits", whereby vigilant users could earn "credits" for their mutes. They could then redeem these credits as subscribers to the program.
