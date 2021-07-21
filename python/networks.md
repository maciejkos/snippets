#python #networkx
How to filter / get edges of a MultiDiGraph by their attribute?

```python
## How to filter / get edges of a MultiDiGraph by their attribute?
multigraph = nx.MultiDiGraph()
# add some edges here
# [.....]

# find edges that meet your criteria
multigraph_d20_d51_edges = list((u, v, d) for u,v,d in multigraph.edges(data=True)
               if d["day_number"] > 20 and d["day_number"] <= 51)

# make a new graph for found edges and add them to it
multigraph_d20_d51 = nx.MultiDiGraph()
multigraph_d20_d51.add_edges_from(multigraph_d20_d51_edges)


```