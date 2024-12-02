## Javascript-MongoDB demo app - developed with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

#### To start the application using docker compose

Step 1: start mongodb

    docker-compose -f docker-compose.yaml up     
    
Step 2: start node server 

    npm install
    node server.js
    
Step 3: access the nodejs application from browser 

    http://localhost:3000
