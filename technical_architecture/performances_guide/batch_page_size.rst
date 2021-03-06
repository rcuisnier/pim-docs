Job product batch size
======================

A product catalog is unique to one's need. It is configured with a custom number of attributes, families, locales, channels, etc. Those different combinations may affect the batch jobs (CSV imports/exports, mass edits, indexation, etc) performances.

Indeed the size of the products will define how much RAM they will take to be processed. During a product batch jobs, we regularly flush the processed products into the database to avoid too much memory consumption.

But, if we flush them too often, the transaction time can slow the process: for each iteration, we clear the doctrine cache (to free some memory), index the products (so more communications between PHP and elastic search) and update the Mysql database. On the other hand, if we flush too sporadically, the RAM consumption can increase to a point where the PHP's garbage collector is called too many times and slows down the batch jobs.

That's why there is no universal answer to the `pim_job_product_batch_size` parameter and if you encounter performance issues on your batch jobs, you may need to tweak it.

To do so, try to increase it if your batch job seems unexpectedly slow and your product have a reasonable size. Or try to reduce it if the batch processes are too slow and your product have a lot of product values.

