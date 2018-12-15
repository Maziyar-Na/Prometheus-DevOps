# Prometheus-DevOps

Introduction to Prometheus
Prerequisites:
Ubuntu 18.04

Commands to run prometheus and the demo:
Go into directory of the project
cd scripts
./install-docker.sh (for installing docker and docker compose)
./install.sh (it will install prometheus and run set of systemd commands to add it as a service)\
  - Verify that it is running by: ps aux | grep prometheus
  - You can check that it is running by typing the url into browser, localhost:9090. (if you run it on localhost)
./install-graphana.sh (it will install Graphana visualization tool, a nicer dashboard, and use systemctl to start it)
  - Verify that Graphana is running by: typing the url, localhost:3000, or executing the command, ps aux | grep graphana
  - The username and password to login to the graphana is: admin, admin
  - Then you can add a new datasource to graphana (Prometheus actually should be the data source in order that graphana get       data from that.) with these configs:
    Name: whatever you want
    Type: Prometheus
    Url: localhost:9090
    Then you can add a dashboard to graphana to start using it. 

For running the Demo:
Go to the directory: flask-prometheus
Execute: docker-compose up -d
docker ps (to make sure that everything is running)
You should now be able to do: curl localhost:5000 and you will see: “flask app is running”
You should be able to execute: curl localhost:5000/query
  - You will see two random numbers (it’s a combination of request to the database and an http request to the app)
You should be able to execute: curl localhost:5000/sleep
  - You will be able to see “done” message after some seconds waiting and it is again a combination of query to the database      and an http request to the flask app which takes more time (regarding the sleep statement in the program)
You should be able to see the metrics which are defined in the program in: localhost:8000
Execute ./add_flask_app.sh (to monitor the app with prometheus)
Restart the prometheus using:
  - ps aux | grep prometheus (for getting the pid of the prometheus process)
  - Kill -HUP <pid> to restart the prometheus service
curl the urls above to send http requests to the app and the database and go to the prometheus dashboard and see the query results in prometheus graph or consul.
The Demo will show you the number of requests and also requests’ latencies both to the app and database. 

