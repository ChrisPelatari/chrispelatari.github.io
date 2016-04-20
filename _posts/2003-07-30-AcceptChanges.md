---
layout: post
title: AcceptChanges()
---
Okay, I'm about to show a little of my ignorance here, but that's okay - at least I'm blogging again.

I just tracked down a bug in some software I wrote that was actually my fault (this time). It had to do with DataSets, their disconnected behavior, and a corresponding method ".AcceptChanges()". When I had originally added this cute little method to my app, I figured that it would fire off a message to the underlying database telling it the changes I've made are accepted.

Wrong. According to MSDN:

When AcceptChanges is called, any DataRow object still in edit mode successfully ends its edits. The DataRowState also changes: all Added and Modified rows become Unchanged; Deleted rows are removed.

and it goes on to say:

The AcceptChanges method is generally called on a DataTable after you attempt to update the DataSet using the DbDataAdapter.Update method.

which, of course, I didn't bother to read the first time 'round. Basically, I was "accepting changes" before the update/insert was made - the bug was not discovered, however, until I tried to put in a new record into the database...I was testing on records which were already entered, and the last method with a straggling .AcceptChanges() method was never called, hence the call was never removed.

The worst part is that I recognized the rush of adrenaline as someone told me something live is "broken" - heh, that could mean just about anything. Thankfully, I knew where the problem child of this beast was - in a monolithic page with too many controls for its own good. Bug found, targeted, searched, destroyed.

HAND.