NodeJS with pm2

WorkDir is /usr/src/apps

ex) docker-compose.yml
volumes:
- /your/app/path:/usr/src/apps

ports:

26000:26000

or if you need more expose port just add more "EXPOSE" to Dockerfile and pm2 process.yml