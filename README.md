# Diskover FileSystem Crawler

Welcome to Diskover FS Crawler 

This crawler helps to index files from your local file system or over nfs mounts.
It crawls your file system and index files and adds to [Amazon Elasticsearch](https://aws.amazon.com/elasticsearch-service/).

# Installation Guide

## Download diskover

```sh
git clone https://github.com/shirosaidev/diskover.git
cd diskcover
```

The distribution contains:

```
$ tree
.
├── LICENSE
├── NOTICE
├── README.md
├── diskover.py
└── diskover.cfg
```


# User Guide

## Getting Started

You need to have at least **Python 2.7.10** and have installed Python client for Elasticsearch using pip:

```sh
pip install elasticsearch
```

Start Diskcover FS crawler with:

```sh
python diskover.py
```

## Diskover CLI options

* `-h, --help` displays help
* `-d, --topdir` directory to start crawling from (default: .)
* `-m, --mtime` minimum days ago for modified time (default: 30)
* `-s, --minsize` minimum file size in MB (default: 5)
* `-t, --threads` number of threads to use (default: 2)


## Config file

Diskcover will read a local config file (`diskover.cfg`).

* `[excluded_dirs]`
* `dirs = .snapshot`

* `[excluded_files]`
* `files = Thumbs.db, .DS_Store, ._.DS_Store, .localized`

* `[aws_es]`
* `host = `

* `[es_index]`
* `name = logstash-diskover`


# Amazon Elasticsearch

## Generated fields

Diskover creates the following fields :

|         Field        |                Description                  |                    Example                  |
|----------------------|---------------------------------------------|---------------------------------------------|
| `last_modified`      | Last modification date                      | `1389220808`                                |
| `last_access`        | Last access date                            | `1482435694`                                |
| `last_change`        | Last change date                            | `1389220808`                                |
| `indexing_date`      | Indexing date                               | `1492612283`                                |
| `filesize`           | File size in bytes                          | `50502536`                                  |
| `filename`           | Original file name                          | `"mypic.png"`                               |
| `extension`          | Original file name extension                | `"png"`                                     |
| `path_parent`        | Parent path name of file                    | `"/tmp/dir1/dir2"`                          |
| `path_full`          | Actual real path name                       | `"/tmp/dir1/dir2/mypic.png"`                |
| `owner`              | Owner name                                  | `"cpark"`                                   |
| `group`              | Group name                                  | `"staff"`                                   |
| `hardlinks`          | Hardlink count                              | `1`                                         |
| `inode`              | Inode number                                | `652490`                                    |


# License

```
This software is licensed under the Apache 2 license, quoted below.

Copyright 2016-2017 Chris Park

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License. You may obtain a copy of
the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations under
the License.
```
