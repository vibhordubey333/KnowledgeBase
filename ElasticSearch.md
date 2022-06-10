# Elastic Search
   - For windows: ./elasticsearch.bat -Ecluster.name="vibhor.tests" -Enode.name=my_first_node
   - For checking health status.
     - localhost:9200/_cat/health?v&pretty
     - localhost:9200
   - Creating indices
     - curl -XPUT 'localhost:9200/products?&pretty'
     - Checking created indices: curl -XGET localhost:9200/_cat/indices?v&pretty
   - Retrieving complete and partial documents
     - curl -X PUT localhost:9200/products/mobiles/3?pretty -H 'Content-Type: application/json' -d '{"name":"Iphone7","reviews":["Super","Awesome"]}'
     - Verify above command using GET call curl -XGET 'localhost:9200/products/mobiles/1?pretty'
   - Excluding certain fields from the response
     - curl -XGET 'localhost:9200/products/mobiles/3?pretty&_source=false'
   - Only want selected fields in response
     - curl -XGET 'localhost:9200/products/mobiles/3?pretty&_source=name,reviews'
   - Updating complete and partial documents[Pay attention to _update keyword]
     - Updating documents
       - curl -X POST localhost:9200/product/laptops/3/_update?pretty -H 'Content-Type: application/json' -d '{"doc":{"color":"black"}}'
       - Fetching above query curl -XGET 'localhost:9200/product/laptops/1?pretty' 
    - Updating particular field using "_script"
      - Let's add the price field
	       curl -X POST localhost:9200/product/laptops/3/_update?pretty -H 'Content-Type: application/json' -d '{"doc":      {"price":15000}}'
	    - Fetching the above field curl -XGET 'localhost:9200/product/laptops/3?pretty'
	    - Doubling the price now.
	       curl -X POST localhost:9200/product/laptops/3/_update?pretty -H 'Content-Type: application/json' -d  '{"script":"ctx._source.price *= 2" }'
	    - Use above command to fetch the updated field.
      - Deleting the documents
      	- curl -XGET 'localhost:9200/product/laptops/1?pretty'
      	- curl -XDELETE 'localhost:9200/product/laptops/1?pretty'
      	- Whenever deletion operation is done it doesn't get deleted instantly. It is marked for deletion then later on when merge  happens behind the scenes to consolidate space then it happens.
	    - To delete the entire index just mention the index.
	      - curl -XDELETE 'localhost:9200/product/laptops?pretty'
       
      -  Performing Bulk Operations
	- Fetch items before performing bulk get call 
	  `curl -XGET 'localhost:9200/product/laptops/1?pretty'`
	- curl --location --request GET 'http://localhost:9200/_mget?pretty' --header 'Content-Type: application/json' --data-raw '{
          "docs": [
			{
			    "_index": "product",
			    "_type": "laptops",
			    "_id": "1"
			}
        	 ]
		}'
