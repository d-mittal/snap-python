GetSccSzCnt
'''''''''''

.. function:: GetSccSzCnt(Graph, SccSzCnt)

Returns a distribution of strongly connected component sizes.

Parameters:

- *Graph*: graph (input)
	A Snap.py graph or a network

- *SccSzCnt*: TIntPrV, a vector of (int, int) pairs (output)
    Vector of pairs (number of nodes in the component, number of such components)

Return Value:

- None

The following example shows how to get the distribution of weakly connected component sizes in
:class:`TNGraph`, :class:`TUNGraph`, and :class:`TNEANet`::

	import snap

	# Directed Graph
	Graph = snap.GenRndGnm(snap.PNGraph, 100, 1000)
	ComponentDist = snap.TIntPrV()
	snap.GetSccSzCnt(Graph, ComponentDist)
	for comp in ComponentDist:
	    print "Size: %d - Number of Components: %d" % (comp.GetVal1(), comp.GetVal2())

	# Undirected Graph
	Graph = snap.GenRndGnm(snap.PUNGraph, 100, 1000)
	ComponentDist = snap.TIntPrV()
	snap.GetSccSzCnt(Graph, ComponentDist)
	for comp in ComponentDist:
	    print "Size: %d - Number of Components: %d" % (comp.GetVal1(), comp.GetVal2())

	# Network
	Graph = snap.GenRndGnm(snap.PNEANet, 100, 1000)
	ComponentDist = snap.TIntPrV()
	snap.GetSccSzCnt(Graph, ComponentDist)
	for comp in ComponentDist:
	    print "Size: %d - Number of Components: %d" % (comp.GetVal1(), comp.GetVal2())
