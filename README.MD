# MONGODB + MONGO-EXPRESS ON DOCKER

## Used Images
```
docker pull mongo
docker pull mongo-express
docker pull alpine
```

Alpine image is only used for checking, whether the backup is in place.  

## Use docker-compose to execute Mongo and Mongo-Express

```
docker-compose up -d
```

- Browse to localhost:8081
- Use the user and password from docker-compose.yaml

## Backup the database 

First stop the container and then run the backup

```
docker-compose stop
docker run --rm --volumes-from mongodb_mongo_1 -v C:\Users\marti\Projects\mongodb:/backup alpine sh -c "cd /data/db && tar cvf /backup/mongodb_datadir.tar ."
```

When you want to delete everything

```
docker-compose rm
docker volume rm mongodb_datadir
```

## Restore the backup

```
docker run --rm -v mongodb_datadir:/recover -v C:\Users\marti\Projects\mongodb:/backup alpine sh -c "cd /recover && tar xvf /backup/mongodb_datadir.tar"
```

## Check the volume

```
docker run --rm -v mongodb_datadir:/data/db alpine sh -c "cd /data/db && ls"
```
