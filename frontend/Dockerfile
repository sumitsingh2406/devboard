#stage1
FROM node:24 as builder

#this is a working directory creating inside the container to run
WORKDIR /app

#copy the packages of node js to run inside the container
COPY package*.json ./

# installation of node package manager (npm) to install the dependencies
RUN npm install  --legacy-peer-deps

#checking vite already exist or not, if not then install the vite@5.4.11
RUN npm list vite >/dev/null 2>&1 || npm install vite@5.4.11

#copy of code to container 
COPY . .

#to run all dependies and store in build folder
RUN npm run build

#stage2
FROM node:26-alpine

WORKDIR /app

#copy of dependies from stage 1 builder from /app/dist folder ( host machine ) and paster to ./dist in continaer
COPY --from=builder /app/dist ./dist

#copy all the modules downloaded in /app/note_module and paste inside the container in ./node_modules
COPY --from=builder /app/note_modules ./node_modules


COPY vite.preview.config.js ./vite.config.js

EXPOSE 4173

CMD ["vite", "preview", "---host","0.0.0.0", "--port", "4173",]
