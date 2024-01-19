---
title: Log-Structured Merge-Trees
---

In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), the **log-structured merge-tree** (also known as **LSM tree**, or **LSMT**[[1]](https://en.wikipedia.org/wiki/Log-structured_merge-tree#cite_note-1)) is a [data structure](https://en.wikipedia.org/wiki/Data_structure "Data structure") with performance characteristics that make it attractive for providing [indexed](https://en.wikipedia.org/wiki/Database_index "Database index") access to files with high insert volume, such as [transactional log data](https://en.wikipedia.org/wiki/Transaction_log "Transaction log"). LSM trees, like other [search trees](https://en.wikipedia.org/wiki/Search_tree "Search tree"), maintain key-value pairs. LSM trees maintain data in two or more separate structures, each of which is optimized for its respective underlying storage medium; data is synchronized between the two structures efficiently, in batches.

One simple version of the LSM tree is a two-level LSM tree.[[2]](https://en.wikipedia.org/wiki/Log-structured_merge-tree#cite_note-2) As described by [Patrick O'Neil](https://en.wikipedia.org/wiki/Patrick_O%27Neil "Patrick O'Neil"), a two-level LSM tree comprises two [tree-like](https://en.wikipedia.org/wiki/Tree_(data_structure) "Tree (data structure)") structures, called C0 and C1. C0 is smaller and entirely resident in memory, whereas C1 is resident on disk. New records are inserted into the memory-resident C0 component. If the insertion causes the C0 component to exceed a certain size threshold, a contiguous segment of entries is removed from C0 and merged into C1 on disk. The performance characteristics of LSM trees stem from the fact that each component is tuned to the characteristics of its underlying storage medium, and that data is efficiently migrated across media in rolling batches, using an algorithm reminiscent of [merge sort](https://en.wikipedia.org/wiki/Merge_sort "Merge sort"). Such tuning involves writing data in a sequential manner as opposed to as a series of separate random access requests. This optimization reduces seek time in [hard-disk drives](https://en.wikipedia.org/wiki/Hard_disk_drive "Hard disk drive") (HDDs) and latency in [solid-state drives](https://en.wikipedia.org/wiki/Solid-state_drive "Solid-state drive") (SSDs).

# Complexity

- Insertion: O(1) amortised
- Find-min: O(N)
- Delete-min: O(N)
# Resources

https://en.wikipedia.org/wiki/Log-structured_merge-tree