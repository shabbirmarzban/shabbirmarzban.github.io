---
layout: post
author: Shabbir Marzban

---
Recently I pulled all the location history Google has collected over the years
on me and I was amazed at the scale of it, there are more than ~2M data points!. I queried on it using [DuckDB](https://duckdb.org/) and visualized it using [KeplerGL](https://kepler.gl/)

```python
!wc -l data.csv 
```
2003568 samples :O

```python
# read the csv file in duckdb
con = duckdb.connect(database=":memory:", read_only=False)
con.install_extension("spatial")
con.load_extension("spatial")
con.install_extension("h3", repository="community")
con.load_extension("h3")

location_data = con.sql(
    """
        WITH date_wise_records as (
            WITH RECORDS as (
                SELECT CAST(latitude AS FLOAT)/1E7 as lat,
                    CAST(longitude AS FLOAT)/1E7 as long, 
                    h3_latlng_to_cell_string(lat,long, 9) as h3,
                    datetrunc('day',timestamp) as date,
                FROM read_csv('data.csv',sep=',', header=True)
            )
            SELECT DISTINCT h3, date FROM RECORDS
        )
        SELECT h3, count(*) as count FROM date_wise_records GROUP BY h3
    """
).df()
``` 
DuckDB being superfast, it execeuted above aggrgation in just 0.5s on 15 year old desktop machine.

``` 
map_1 = KeplerGl(height=800)
map_1.add_data(data=location_data, name="location_data")
map_1
``` 
Here is the nice map :D
<iframe src="{{ '/assets/location_data.html' | relative_url }}" width="100%" height="600px" frameborder="0"></iframe>

Enjoy ;)