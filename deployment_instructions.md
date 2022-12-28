# Requirements: 
- mongodb 
- maven 
- java 1.8 (sdk, jre, jdk, etc) 
- tomcat (if you'd like to deploy the web frontend locally) 


# Deploying mrp 
1. Run mongodb (hint: you should run `mongod` and have an open console showing db logs/output`
2. Run the following sequence of commands:

```
// to seed the database...
cd deploy/
mongo localhost:27017/ordering MongoRecords.js

// to compile the web frontend and copy it to the docker dir
cd - 
cd src/Clients
chmod +x gradlew
./gradlew build

// if you'd like to deploy the frontend using docker (to avoid downloading tomcat)...
cp build/libs/mrp.war ../../deploy/docker/Clients/drop/
cd ../../deploy/docker
chmod +x *.sh
./BuildAndRun.sh

// you should now check if the app is running at localhost:80/mrp

// to compile + run the backend (locally only) 
cd -
cd src/Backend/OrderService
mvn clean
mvn install -DskipTests
chmod +x run.sh
./run.sh

// app should be running now!
```
