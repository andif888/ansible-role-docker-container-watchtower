# ansible-role-docker-container-watchtower

Role to run watchtower in a docker container

## Table of content

- [Default Variables](#default-variables)
  - [docker_container_watchtower_debug](#docker_container_watchtower_debug)
  - [docker_container_watchtower_env](#docker_container_watchtower_env)
  - [docker_container_watchtower_image](#docker_container_watchtower_image)
  - [docker_container_watchtower_label_enable](#docker_container_watchtower_label_enable)
  - [docker_container_watchtower_labels](#docker_container_watchtower_labels)
  - [docker_container_watchtower_log_level](#docker_container_watchtower_log_level)
  - [docker_container_watchtower_monitor_only](#docker_container_watchtower_monitor_only)
  - [docker_container_watchtower_name](#docker_container_watchtower_name)
  - [docker_container_watchtower_networks](#docker_container_watchtower_networks)
  - [docker_container_watchtower_notification_url](#docker_container_watchtower_notification_url)
  - [docker_container_watchtower_notifications_hostname](#docker_container_watchtower_notifications_hostname)
  - [docker_container_watchtower_notifications_level](#docker_container_watchtower_notifications_level)
  - [docker_container_watchtower_notifications_title_tag](#docker_container_watchtower_notifications_title_tag)
  - [docker_container_watchtower_ports](#docker_container_watchtower_ports)
  - [docker_container_watchtower_schedule](#docker_container_watchtower_schedule)
  - [docker_container_watchtower_timezone](#docker_container_watchtower_timezone)
  - [docker_container_watchtower_volume_dir](#docker_container_watchtower_volume_dir)
  - [docker_container_watchtower_volumes](#docker_container_watchtower_volumes)
  - [docker_image_watchtower_name](#docker_image_watchtower_name)
  - [docker_image_watchtower_pull](#docker_image_watchtower_pull)
  - [docker_network_watchtower_name](#docker_network_watchtower_name)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### docker_container_watchtower_debug

Enable debug mode with verbose logging.

#### Default value

```YAML
docker_container_watchtower_debug: 'false'
```

### docker_container_watchtower_env

Dictionery of key,value pairs for docker environment variables to configure watchtower.

Example:

```yaml

docker_container_watchtower_env:

WATCHTOWER_MONITOR_ONLY: "true"

```

#### Default value

```YAML
docker_container_watchtower_env:
  WATCHTOWER_DEBUG: '{{ docker_container_watchtower_debug }}'
  WATCHTOWER_LABEL_ENABLE: '{{ docker_container_watchtower_label_enable }}'
  WATCHTOWER_LOG_LEVEL: '{{ docker_container_watchtower_log_level }}'
  WATCHTOWER_MONITOR_ONLY: '{{ docker_container_watchtower_monitor_only }}'
  WATCHTOWER_NOTIFICATIONS_HOSTNAME: '{{ docker_container_watchtower_notifications_hostname
    | default(omit) }}'
  WATCHTOWER_NOTIFICATIONS_LEVEL: '{{ docker_container_watchtower_notifications_level
    }}'
  WATCHTOWER_NOTIFICATION_TITLE_TAG: '{{ docker_container_watchtower_notifications_title_tag
    | default(omit) }}'
  WATCHTOWER_NOTIFICATION_URL: '{{ docker_container_watchtower_notification_url }}'
  WATCHTOWER_SCHEDULE: '{{ docker_container_watchtower_schedule }}'
  TZ: '{{ docker_container_watchtower_timezone }}'
```

### docker_container_watchtower_image

Repository path and tag used to create the container. If an image is not found or pull is true, the image will be pulled from the registry. If no tag is included, latest will be used.

#### Default value

```YAML
docker_container_watchtower_image: '{{ docker_image_watchtower_name }}'
```

### docker_container_watchtower_label_enable

Update containers that have a com.centurylinklabs.watchtower.enable label set to true.

#### Default value

```YAML
docker_container_watchtower_label_enable: 'false'
```

### docker_container_watchtower_labels

Dictionary of key value pairs for container labels.

Example:

```yaml

docker_container_watchtower_labels:

traefik.enable: "true"

```

#### Default value

```YAML
docker_container_watchtower_labels: {}
```

### docker_container_watchtower_log_level

The maximum log level that will be written to STDERR (shown in docker log when used in a container).

#### Default value

```YAML
docker_container_watchtower_log_level: info
```

### docker_container_watchtower_monitor_only

Will only monitor for new images, send notifications and invoke the pre-check/post-check hooks, but will not update the containers.

#### Default value

```YAML
docker_container_watchtower_monitor_only: 'true'
```

### docker_container_watchtower_name

Name for the container

#### Default value

```YAML
docker_container_watchtower_name: watchtower
```

### docker_container_watchtower_networks

List of networks the container belongs to.

#### Default value

```YAML
docker_container_watchtower_networks:
  - name: '{{ docker_network_watchtower_name }}'
```

### docker_container_watchtower_notification_url

The shoutrrr service URL to be used. This option can also reference a file, in which case the contents of the file are used. Go to https://containrrr.dev/shoutrrr/v0.6/services/overview to learn more about the different service URLs you can use. You can define multiple services by space separating the URLs. Example: smtp://username:password@host:port/?from=fromAddress&to=recipient1[,recipient2,...]

#### Default value

```YAML
docker_container_watchtower_notification_url: ''
```

### docker_container_watchtower_notifications_hostname

Custom hostname specified in subject/title. Useful to override the operating system hostname

### docker_container_watchtower_notifications_level

Controls the log level which is used for the notifications. If omitted, the default log level is info. Possible values are: panic, fatal, error, warn, info, debug or trace.

#### Default value

```YAML
docker_container_watchtower_notifications_level: info
```

### docker_container_watchtower_notifications_title_tag

Custom hostname specified in subject/title. Useful to override the operating system hostname

### docker_container_watchtower_ports

List of ports to publish from the container to the host.

#### Default value

```YAML
docker_container_watchtower_ports: []
```

### docker_container_watchtower_schedule

Cron expression in 6 fields (rather than the traditional 5) which defines when and how often to check for new images.

#### Default value

```YAML
docker_container_watchtower_schedule: '* 1 2 * * *'
```

### docker_container_watchtower_timezone

Sets the time zone to be used by WatchTower's logs and the optional Cron scheduling argument (--schedule).

#### Default value

```YAML
docker_container_watchtower_timezone: UTC
```

### docker_container_watchtower_volume_dir

Volume mount host directory, where Treafik config files are stored.

#### Default value

```YAML
docker_container_watchtower_volume_dir: '{{ docker_container__base__volume_dir }}/{{
  docker_container_watchtower_name }}'
```

### docker_container_watchtower_volumes

List of volumes to mount within the container.

#### Default value

```YAML
docker_container_watchtower_volumes:
  - /var/run/docker.sock:/var/run/docker.sock
```

### docker_image_watchtower_name

Repository path and tag for the container image.

#### Default value

```YAML
docker_image_watchtower_name: containrrr/watchtower:latest
```

### docker_image_watchtower_pull

Indicate to always pull the docker image.

#### Default value

```YAML
docker_image_watchtower_pull: no
```

### docker_network_watchtower_name

Name of the docker network created for watchtower.

#### Default value

```YAML
docker_network_watchtower_name: '{{ docker_container_watchtower_name }}_backend'
```

## Discovered Tags

**_docker-container-prereq-all_**\
&emsp;Ensure all pre-requisites are installed

**_docker-container-prereq-watchtower_**\
&emsp;Ensure all pre-requisites for watchtower are installed

**_docker-container-purge-all_**\
&emsp;Remove all containers and delete volume mounts.

**_docker-container-purge-watchtower_**\
&emsp;Remove watchtower and delete volume mounts.

**_docker-container-remove-all_**\
&emsp;Remove all containers.

**_docker-container-remove-watchtower_**\
&emsp;Remove watchtower.

**_docker-container-setup-all_**\
&emsp;Run setup task for all containers.

**_docker-container-setup-watchtower_**\
&emsp;Run setup task for watchtower.

**_never_**


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
