Columnar Store
===

Context: data architecture

Problem: how do I store data when I'm often interested in a subset of the columns of all rows?

Solution: group data by column, not by row. Column stores can very quickly operate on subsets of data as these subsets are stored close to each other.
