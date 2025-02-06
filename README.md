**Struction app**

![image](https://github.com/user-attachments/assets/a204383c-d236-4727-9807-bc4f03814ad2)

  - _**user.js**_ in **models** folder

 **Write Dockerfile**

     # Use official Node.js image
     FROM node:18

     # Set the working directory
     WORKDIR /app

     # Install dependencies
     COPY package.json package-lock.json ./
     RUN npm install

     # Copy the rest of the application files
     COPY . .

     # Expose the port
     EXPOSE 3000

     # Start the app
     CMD ["node", "server.js"]


**Write .env**

    DB_HOST=${DB_HOSTS}
    DB_USER=${DB_USER}
    DB_PASSWORD=${DB_PASSWORD}
    DB_NAME=${DB_NAME}
    DB_PORT=${DB_PORT}
    PORT=${PORT}

**Login DockerHub**

    docker login --username asdxxyy

**Create docker image and push DockerHub**

    docker build -t asdxxyy/nodejs .

    docker pull asdxxyy/nodejs

**Create Secret in Kubernetes**

    kubectl create secret generic secjs --from-literal DB_PASSWORD=123 --from-literal DB_USER=userjs --from-literal DB_NAME=dbjs --from-literal PORT=3000 --from-literal DB_HOSTS=192.168.182.151 --from-literal DB_PORT=5432

**Create Deployment in Kubernetes**

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      creationTimestamp: null
      labels:
        app: deploy-node
      name: deploy-node
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: deploy-node
      strategy: {}
      template:
        metadata:
          creationTimestamp: null
          labels:
            app: deploy-node
        spec:
          containers:
          - image: ulugbekit94/nodejs
            name: nodejs
            envFrom:
            - secretRef:
                name: secjs
            ports:
            - containerPort: 3000
            resources: {}
    status: {}

-------------------------------------------------------------------------------------------------------------------------------------
