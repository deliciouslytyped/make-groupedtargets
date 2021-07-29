Note: this text was pulled from an issue post without editing, the phrasing may be odd.

This post is going to be a bit off topic, but it seems as good a place as any to summarize some things;

this seems like one of those somewhat more obscure features of make that ~~is~~(was?) bafflingly missing decent support.
**Edit:** (I mean in make itself, not remake.)
~~With the research I've been able to manage, things do seem to point to gmake's pattern rules being the cleanest, albeit still hacky solution to multiple-output targets.~~ This may have been fixed by "grouped targets" in 4.3, see [3] and [4].

A link I haven't seen mentioned here yet is https://www.gnu.org/software/automake/manual/html_node/Multiple-Outputs.html , which goes quite in depth with the pertinent issues. (It is also this article which leads to my bafflement to the lack of a decent solution; you can't expect everyday developers to have to deal with this, and I myself don't understand the contents of that article yet). Given that it's in the automake documentation, maybe automake has support for dealing with this, but I haven't gotten to the point of researching that.

Perhaps the issues listed in that document are also a good test for remakes debugging capabilities.

To aggregate some of the above, the most useful things I've found on the topic so far are:
[1] https://www.gnu.org/software/automake/manual/html_node/Multiple-Outputs.html
[2] https://www.cmcrossroads.com/article/rules-multiple-outputs-gnu-make - as linked previously (I actually found this because I didn't believe that was pattern rules were really gmake's solution...)
[3] https://lists.gnu.org/archive/html/info-gnu/2020-01/msg00004.html linked above, has some content:
```

* New feature: Grouped explicit targets
  Pattern rules have always had the ability to generate multiple targets with
  a single invocation of the recipe.  It's now possible to declare that an
  explicit rule generates multiple targets with a single invocation.  To use
  this, replace the ":" token with "&:" in the rule.  To detect this feature
  search for 'grouped-target' in the .FEATURES special variable.
  Implementation contributed by Kaz Kylheku <address@hidden>
```
This looks interesting, and I should look into it. If not for this thread, I don't think I would have ever found this.
Grouped targets appear to be documented at 
[4] https://www.gnu.org/software/make/manual/html_node/Multiple-Targets.html

There is a little bit of exposition at https://stackoverflow.com/a/63935393 and a common pitfall seems to be trying to use it with older versions: https://stackoverflow.com/a/63162448 , https://stackoverflow.com/questions/61345698/gnu-make-grouped-targets-are-not-grouped

Here is a proposed solution for the lack of an automatic variable expanding to all grouped targets; https://stackoverflow.com/questions/60402075/is-there-an-automatic-variable-for-all-grouped-targets-in-makefile/60441626#60441626

https://lwn.net/Articles/810247/ reports to have a portable implementation of grouped targets at https://github.com/david-a-wheeler/make-booster

Also I should probably correct my terminology, people seem to say `multi-target`, though I don't think that's obviously the same thing as `multi-output`. Maybe the term is now `grouped targets`.


- [ ] If indeed grouped targets are what's wanted for multiple-outputs, the automake documentation should be updated to reflect this.

Now if only `The GNU Make Book` or `Managing Projects With GNU Make` was updated. :)

If anyone has any additional resources to add to this list, that would be cool; please open an issue or a PR.
