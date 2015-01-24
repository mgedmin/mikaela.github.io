---
layout: post
title: "Getting help from network operators with channel issues when ops are away"
category: [english]
tags: [oper, irc, groupserv, hostserv]
---

In case you wish network operators to help you when your channel operators
are away, please authorize them to do so. You can do this simply by
command `/msg ChanServ flags #channel $oper +vhoirtAe`. *Note that this
assumes that your network uses Atheme with exttarget $oper loaded.*

If you don't do this and there is trouble on your channel, it can be
assumed that you don't want network operators to intervene and they most
likely take no action. Taking action would also require using operator
privileges such as `/samode` which might not be so nice unless the flags
are set.

I repeat that the commnd is `/msg ChanServ flags #channel $oper +vhoirtAe`.
The only thing that must be changed is `#channel`.

## Explanation of these flags

* v - allows using voice/devoice commands
* h - allows using halfop/dehalfop commands
* o - allows using op/deop commands
* i - allows using invite/getkey commands
* r - allows using kick/kickban/ban/unban commands
* t - allows using topic/topicappend commands
* A - allows seeing channel access lists and (MemoServ) sendops command
    * most of our alerts seem to be coming from opers who are accidentally
      using their priviledges and seeing access list of channel they have
      no access to.
    *  `<ChanServ> Mikaela ACCESS:LIST: #channel (oper override)`
* e - exempts from akick and allows unbanning yourself

**NOTE THAT FLAGS ARE CASE-SENSITIVE**

### Effects of misspelled flags

Some flags change their meaning if written with wrong case:

* V - automatic voice and allows using voice/devoice on yourself
* H - automatic halfop and allows using halfop/dehalfop on yourself
* O - automatic op and allows using op/deop on yourself
* R - allows using recover, sync and clear commands
    * recover - deop everyone, remove key, invite yourself, add ban
      exception on yourself, unban yourself, set modes +im (invite-only,
      only voiced users can talk), op yourself and other fun...
    * sync - sync the channel according to access list
    * clear - allows clearing akicks (+b flags), bans, flags, users
      (=kick everyone)

So you don't want to accidentally confuse different letters. `+VHOR` aren't
so dangerous and you can freely set them, but avoid confusing +r and +R.

## One last note

`$oper` matches everyone who is opered and requires Atheme to have
exttarget $oper loaded. Some other networks use different ways to add opers
to be on access list.

* queertech: `$oper` should work for you, but there is also `!netadmins`
  which only includes netadmins and matches them even if they aren't
  opered.
* freenode: no `$oper`, it's adviced to use `*!*@freenode/staff/*`.