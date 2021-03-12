# Al-Folio with Docker

This is intended to allow users to develop their own [al-folio](https://github.com/alshedivat/al-folio) websites using Docker.

**Why would I do that?**

Great question. While it's recommended you simply install everything on your own computer, this can be useful for those who cannot or do not want to install the software and those interested in quickly trying out al-folio.

## Steps:

1. Fork the theme so you have your own site. Fork the theme from `github.com:alshedivat/al-folio` to `github.com:<your-username>/<your-repo-name>`. Download the repo somewhere on your local disk (`git clone <url of your al-folio repo>`).

2. Edit the `docker-compose.yml`. All you need to do is provide the full path of the local copy of your repo (where you cloned it in the last step). Enter this in the volume section under the comment `# full path to the local copy of your github repo`.

3. Start the container. You can start the container with `docker-compose up -d` and then "enter" the container with `docker-compose exec site bash`.

4. Change directories to your site folder. You can do this with `cd /root/my-al-folio-site`.

5. Install the necessary gems with `bundle install`.

6. To launch the site use `bundle exec jekyll serve`. The terminal should look like:

```
bundle exec jekyll serve
Configuration file: /root/al-folio/_config.yml
            Source: /root/al-folio
       Destination: /root/al-folio/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
         AutoPages: Disabled/Not configured in site.config.
        Pagination: Complete, processed 1 pagination page(s)

 Auto-regeneration: enabled for '/root/my-al-folio-site'
    Server address: http://127.0.0.1:4000/my-al-folio-site/
  Server running... press ctrl-c to stop.
```

There may be warnings somewhere in between all of that. You should be able to access the site from your computer's browser at the server address listed in the command.

To stop it, you can use control+c (at least on linux). To leave the container you can use `exit`. Once you are out of the container you can use `docker-compose down` to bring the container down.

For more details on the site, check out https://github.com/alshedivat/al-folio. I recommend starting with `_config.yml` where you can set the title and social information. The files of your repo are mounted within the docker volume, so you can edit them using the software of your choice on your computer and the changes will be reflected within the container. You may have to stop the `bundle exec jekyll serve` with control+c and then run the command again for the changes to be reflected.

## Docker Image

I put the docker image for this [on DockerHub](https://hub.docker.com/repository/docker/alexandermichels/al-folio-docker) to make it easier for users. The Dockerfile is in `src/dockerfiles` for those who want to build the image themselves for any reason.
