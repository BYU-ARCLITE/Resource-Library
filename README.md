# README #

This is deployment configuration for the Ayamel Media Resource API.

> Note: Before you use, or work on this config, make sure to activate the `common-ansible` repo into `common/` as a git submodule:

>   `git submodule update --init`

## Conventions ##

All playbooks are organized in subdirectories based on their intended use:

* `tasks/system` - playbooks for configuring an individual system

## Examples ##

To configure and deploy the project on the staging environment:
    
    # set up staging environment, and then deploy
    ansible-playbook configure-staging.yml
    ansible-playbook deploy-staging.yml

Or to see what might get changed if you were to configure the production environment:

    # run entire staging deploy
    ansible-playbook configure-production.yml --check
    
## Servers ##

### Proxy ###

Runs HAProxy, handling SSL and forwarding actual requests on to the web servers.

### Web & Task ###

These servers contain the application code, which is Symfony2 in PHP, but not much else.

The web servers also have *nginx* and *php-fpm* for serving the app to the web, wheras the 
task and transcoding servers do not serve to the web, and only run tasks asynchronously.

### DB Servers ###

DB servers just contain MongoDB.  This will become considerably more complex later, as mongo is properly configured for sharding
and replica sets.

### Task ###

Responsible for running background tasks, primarily transcoding.

### Queue ###

Runs RabbitMQ

### Search ###

Runs ElasticSearch
