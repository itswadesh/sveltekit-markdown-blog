---
title: Complete steps to configure elasticsearch on Ubuntu
published: '2021-02-17T00:00:00.000+08:00'
updated: '2021-02-17T12:00:00.000+08:00'
tags: ['elastic search', 'ubuntu']
series: false
cover: ./elasticsearch.png
canonical_url: false
description: 'Here are complete steps to get started with elasticsearch on Ubuntu machine'
---

Here are complete steps to get started with elasticsearch on Ubuntu machine

## Step-1: Install Java

```
sudo apt-get update
sudo apt-get install oracle-java11-installer-local
sudo apt-get install oracle-java11-set-default-local
```

To uninstall Java

```
sudo apt-get purge oracle-java11-set-default-local
```

Check if java installed properly

```
java -version
echo $JAVA_HOME
```

## Step-2: Install elastic search

```
sudo apt-get install apt-transport-https
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
add-apt-repository "deb https://artifacts.elastic.co/packages/7.x/apt stable main"
sudo apt-get update
sudo apt-get install elasticsearch
```

## Step-3: Configure elasticsearch

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Change the fllowing

```
cluster.initial_master_nodes: node-1
network.host: ["0.0.0.0, 127.0.0.1,[::1]"]
network.bind_host: 0.0.0.0
network.publish_host: 0.0.0.0
http.host: 0.0.0.0
```

## Step-4: Setup JVM options based on available RAM

```
nano /etc/elasticsearch/jvm.options
```

Change the following values

```
-Xms256m
-Xmx256m
```

## Step-5: Start elasticsearch service

```
service elasticsearch start
service elasticsearch status
```

## Step-6: Verify elasticsearch running

```
curl -X GET "http://localhost:9200/?pretty"
```

You should get the following output

```
{
    "name": "litekart",
    "cluster_name": "elasticsearch",
    "cluster_uuid": "uGqoSysyQN-tJMxq3reiXg",
    "version": {
        "number": "7.4.2",
        "build_flavor": "default",
        "build_type": "deb",
        "build_hash": "2f90bbf7b93631e52bafb59b3b049cb44ec25e96",
        "build_date": "2019-10-28T20:40:44.881551Z",
        "build_snapshot": false,
        "lucene_version": "8.2.0",
        "minimum_wire_compatibility_version": "6.8.0",
        "minimum_index_compatibility_version": "6.0.0-beta1"
    },
    "tagline": "You Know, for Search"
}
```

### Setup password to secure elastic search instance

- Verify that the xpack.security.enabled setting is true on each node in your cluster.

  -- sudo nano /etc/elasticsearch/elasticsearch.yml

```
xpack.security.enabled
```

```
cd /usr/share/elasticsearch
./bin/elasticsearch-setup-passwords
```
