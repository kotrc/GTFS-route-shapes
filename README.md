# GTFS-route-shapes
A simple script to generate a single geoJSON shape for each transit route in a GTFS archive.

### Why you might need this
In developing web and mobile applications with public transit data, we often want to display the route of a particular line on a map — let's take the MBTA Red Line in Boston as an example. The way the [GTFS](https://developers.google.com/transit/gtfs/?hl=en) standard organizes data on the map shape of transit lines, however, makes that a little tricky. There are two problems: 

1. Rather than providing the map shape of a route, GTFS provides the map shape of trips, of which one route may have many (see [this](http://blog.openplans.org/wp-content/uploads/2012/08/image30471.png) very helpful sketch of the GTFS schema if that sounds confusing to you). This means a route may have many lines associated with it, usually redundant and overlapping. For example, the MBTA Red Line has two branches in the south, which look like this:
2. 
  ![Map of the MBTA Red Line Braintree branch](/readme-images/Braintree.png?raw=true "Braintree branch")
  ![Map of the MBTA Red Line Ashmont branch](/readme-images/Ashmont.png?raw=true "Ashmont branch")

We can overplot both lines, but then we're dealing with redundant points between the northern terminus (Alewife station) and the branch point. Not a huge deal if there's just two shapes, but for many GTFS archives, a route has _many_ such shapes — the whole shapes.txt table for the MBTA GTFS archive is >17 MB. We really want to store the minimal collection of non-overlapping lines that describe the shape of the whole route:

  ![Map of both MBTA Red Line branches](/readme-images/Both.png?raw=true "Both branches")

2. 
