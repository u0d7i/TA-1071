FROM node:16
RUN apt -y update && apt -y install adb && apt clean
WORKDIR /app
ADD https://gitlab.com/suborg/gdeploy/-/raw/master/package.json /app/
RUN npm install
ADD https://gitlab.com/suborg/gdeploy/-/raw/master/main.js /app/
ENTRYPOINT ["node", "main.js"]
