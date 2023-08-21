https://forum.obsidian.md/t/help-with-group-and-sort-with-dataview-plugin/28649/2


---

Hi.

Your query:

```dataview
LIST rows.file.link
FROM "6.Projects"
WHERE !contains(file.folder, "_Archive") AND !contains(file.name, "_Working on")
GROUP BY file.folder
```
About sorting, some tips (with a “practical” language - I’m not coder too, just more one newbie…):

When using group by, sorting is more complex. The main level to sort are the groups itself. Let’s say you want to sort the output of the groups (not the content in each group). To do that the first idea is: SORT file.folder ASC. Don’t ask me why, but with groups this doesn’t work. You need to do this: first, render group fields to other name using AS syntax (GROUP BY file.folder AS Example); second, sorting using the rendered name (SORT Example DESC)
```dataview
LIST rows.file.link
FROM "6.Projects"
WHERE !contains(file.folder, "_Archive") AND !contains(file.name, "_Working on")
GROUP BY file.folder AS Example
SORT Example DESC
```
Sorting the elements inside a group (without using FLATTEN) demands other direct approach: not using the global SORT but sorting directly the array/list inside groups (in this case rows.file.link) using the function sort(), i.e.:
```dataview
LIST sort(rows.file.link)
FROM "6.Projects"
WHERE !contains(file.folder, "_Archive") AND !contains(file.name, "_Working on")
GROUP BY file.folder
```
sort() gives a default asc natural order. If you need a desc order, you need to use the reverse() function (most of the time together with sort() - reverse(sort(rows.file.link)) - something like “first it’s necessary to order asc and then reverse that order”).

https://blacksmithgu.github.io/obsidian-dataview/query/functions/#sortlist 264

I hope this helps.