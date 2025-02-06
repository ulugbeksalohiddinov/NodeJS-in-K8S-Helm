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


