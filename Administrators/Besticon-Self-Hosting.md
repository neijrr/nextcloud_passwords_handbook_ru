[Besticon](https://github.com/mat/besticon) is a favicon service written in Go which can be used to fetch icons for websites.
The passwords app offers an integration to connect with a server hosting the service.

## Running your own instance of Besticon

### With Heroku
1. [Create](https://signup.heroku.com/) or [log into](https://id.heroku.com/login) your Heroku account.
2. Click [this link](https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon&template=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon).
3. Choose an app name and click "Deploy app".
4. Click on "View" to view the app.
5. Now [configure the app](#configure-the-app).

### With Docker
Please note that we expect you to have [docker](https://get.docker.com/) installed.
You need to run these commands on your server an you need to know the domain of your server.

1. Pull the image: `docker pull matthiasluedtke/iconserver`.
2. Start the container `docker run -d --restart=on-failure -p 8080:8080 --name=besticon matthiasluedtke/iconserver`.
   - If you do not want to user port 8080, replace `-p 8080:8080` with `-p <yourport>:8080`.
3. Open the frontend on port 8080.
   - If the frontend does not work, but the container is running (see `docker ps`), check the logs and your firewall.
   - We do not recommend making the container accessible to the web.
4. Now [configure the app](#configure-the-app).

### With Docker Compose
Please note that we expect you to have [docker](https://get.docker.com/) and [docker-compose](https://docs.docker.com/compose/install/) installed.

1. The docker-compose.yml file:
```yaml
version: '2'

services:
  nextcloud-besticon:
    image: matthiasluedtke/iconserver
    container_name: "nextcloud-besticon"
#    environment:
#      PORT: Your Port Here
```
2. Run `docker-compose up -d`
3. Open the frontend on port 8080,
   - If the frontend does not work, but the container is running (see `docker ps`), check the logs and your firewall.
   - We do not recommend making the container accessible to the web.
4. Now [configure the app](#configure-the-app).
   
   
## Configure the app
1. Open the admin settings of the passwords app ("Settings" > "Passwords") in your Nextcloud.
2. Set "Favicon Service" to "Besticon (recommended)".
3. Set the "Favicon Service Api" to `http://your_domain_or_ip:8080/icon`
   - If you use https or a custom port update the domain accordingly.
4. Reload the page
5. Clear the cache "Favicon"
6. To test the settings
   1. Press F12 in your browser
   2. Open the "Network" tab
   3. Check the "Disable Cache" option
   4. Open the passwords app and check if favicons appear. You can filter for requests with `passwords/api/1.0/service/favicon`
