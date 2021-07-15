# Working out a percentage

I was struggling to get the labels to expose on the value, I am not sure how I came across this solution, I think I lucked out on the group_left part, but it somehow works.

```
((sum(azdo_workitem_tag{project="x",tag=~"Team: .*"}) by (tag) / ignoring(project,tag) group_left sum(azdo_workitem_detail{project="x"})) * 100) > 0.5
```
Set `ignoring` to the filters on the primary value, I would think on does the opposite.
