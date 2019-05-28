---
layout: post
title:  "High-throughput calculations of catalytic properties of bimetallic alloy surfaces!"
date:   2019-05-28 16:30:00
categories: jekyll update
---

Finally, our data descriptor on high-throughput calculations of catalytic properties on bimetallic 
alloy surface is availbale online in this [nature scientific data article][bimetallic_url]. Here, we present
a well curated dataset of catalytic properties, e.g., adsorption energies of C, H, N etc., on a vast set of 
bimetllic alloy surfaces. This dataset is primarily generated to enable machine learning model generation and
data validation for future computational catalysis research.  

To make this data more easily accessible, we develop both a [web API][cathub_bimetal] and [python API][cathub_github]. Interested researcher can clone the github repo and then using few lines of code (shown in the snippet below), anyone can get the data from a python console. 

{% highlight python %}
>>> from cathub.query import get_reactions
>>> data = get_reactions(n_results="all",
                         pubID="MamunHighT2019",
                         reactants="H2",
                         products="H",
                         columns=["SurfaceComposition", "reactionEnergy",
                                  "sites", "reactants", "products"])
Connecting to database at http://api.catalysis-hub.org/graphql
Executing query:
{reactions(pubID: "MamunHighT2019", reactants: "H2", products: "H"){
 totalCount
  edges {
    node {
      SurfaceComposition
      reactionEnergy
      sites
      reactants
      products
     }
   }
}}
Getting data from server ...
Data fetched!
{% endhighlight %}

This code snippet will fetch the data as a `node` where each `node` will contain 
a single adsorption energy computation on a specific surface specified by `SurfaceComposition`, and specific site
speicfied by the `sites` key. If anyone wants to fetch the raw quantum chemistry output file, i.e, Quantum Espresso `pw.pwo` file, please use the following code snippet:

{%highlight python%}
from cathub.query import get_logfile

get_logfile(aseId=info[6], fname=fname + '/pw.pwo')
{%endhighlight%}

where, `aseId` is the unique ase ID of the calculation you want to get and `fname` is the filename that you want to save.


[bimetallic_url]: https://www-nature-com/articles/s41597-019-0080-z
[cathub_bimetal]: https://www.catalysis-hub.org/publications/MamunHighT2019
[cathub_github]: https://github.com/SUNCAT-Center/CatHub/tree/master/cathub
