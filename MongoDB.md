0. Docker `docker run -d -p 27017:27017 --name=mongo-example mongo:latest`
1. Docker exec `docker exec -it container_id sh`
2. Launching shell: `mongosh`
3. Display DB's `show dbs`
4. Switch to database `use courses`
5. `show collections`
6. To list complete collection `db.courses.find()`
