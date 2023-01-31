# Virtual Warehouse Scaling #

* As queries are submitted, resources are calculated and reserved prior to the query execution
* When there are insufficient resources, queries are queued until previous queries finish and release resources

## Scaling Up ##
> Scaling Up: Resizing a warehouse to handle **more complex or data-intensive queries**.

| Warehouse Size | Servers | Clusters |
|:--------------:|:-------:|:--------:|
|    X-Small     |    1    |    1     |
|     Small      |    2    |    1     |
|     Medium     |    4    |    1     |
|     Large      |    8    |    1     |
|    X-Large     |   16    |    1     |
|    2X-Large    |   32    |    1     |
|    3X-Large    |   64    |    1     |
|    4X-Large    |   128   |    1     |

* Scaling up/down is done by changing the size of the warehouse which affects the number of servers in the warehouse cluster 
* A warehouse that is too large may waste compute credits if its resources are not fully utilized
* A warehouse that is too small may become very slow since it may be resource bound, resulting in spilling data to local or remote disk, further degrading performance.

## Scaling Out ##
> Scaling Out: Adding more clusters to the warehouse _without_ changing its size to handle **high concurrency loads**.

Multi-cluster warehouses can work in
* Maximized Mode
  * the minimum and maximum number of clusters is the same and is more than one
  * useful for predictable periods of sustained high loads
* Autoscaling Mode
  * the minimum and maximum number of clusters are different
  * The warehouse will automatically scale up and down (auto-scale) depending on load
  * helps to automate the handling of variable number of queries or users over time
  * Scaling policies
    * Standard
      * useful for relatively smooth transitions from low to high load and back 
      * a new cluster is added
        * as soon as queries start queueing, or
        * an incoming query will be queued due to shortage of resources
      * a cluster is shut down after 2-3 consecutive checks (one minute apart) show that the load on the least-busy cluster can be redistributed to other clusters
    * Economy
      * useful for erratic transitions from low to high load and back, reduces scale out/in reactions to short-lived load spikes or drops
      * a new cluster is added
        * after a query has been queued for up to 6 minutes, or
        * when Snowflake determines that the current work load will keep available clusters busy for at least 6 minutes
      * a cluster is shut down after 5-6 consecutive checks (one minute apart) show that the load on the least-busy cluster can be redistributed to other clusters

## Scaling Considerations ##
* Query processing cannot cross clusters, so, even though the number or clusters is the same, a complex query will perform differently on a 4-cluster multi-cluster warehouse made of `X-Small` clusters compared to a `Medium` warehouse.