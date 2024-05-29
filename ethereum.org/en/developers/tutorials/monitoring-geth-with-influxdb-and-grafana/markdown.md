Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Monitoring Geth with InfluxDB and Grafana

clientsnodes

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Mario
Havel

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
January 13, 2021

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)4
minute read minute read

On this page

  * Prerequisites
  * Monitoring stack
  * Setting up InfluxDB
  * Preparing Geth
  * Setting up Grafana

This tutorial will help you set up monitoring for your Geth node so you can
better understand its performance and identify potential problems.

## Prerequisites

  * You should already be running an instance of Geth.
  * Most of the steps and examples are for linux environment, basic terminal knowledge will be helpful.
  * Check out this video overview of Geth's suite of metrics: [Monitoring an Ethereum infrastructure by Péter Szilágyi(opens in a new tab)](https://www.youtube.com/watch?v=cOBab8IJMYI).

## Monitoring stack

An Ethereum client collects lots of data which can be read in the form of a
chronological database. To make monitoring easier, you can feed this into data
visualisation software. There are multiple options available:

  * [Prometheus(opens in a new tab)](https://prometheus.io/) (pull model)
  * [InfluxDB(opens in a new tab)](https://www.influxdata.com/get-influxdb/) (push model)
  * [Telegraf(opens in a new tab)](https://www.influxdata.com/get-influxdb/)
  * [Grafana(opens in a new tab)](https://www.grafana.com/)
  * [Datadog(opens in a new tab)](https://www.datadoghq.com/)
  * [Chronograf(opens in a new tab)](https://www.influxdata.com/time-series-platform/chronograf/)

There's also [Geth Prometheus Exporter(opens in a new
tab)](https://github.com/hunterlong/gethexporter), an option preconfigured
with InfluxDB and Grafana. You can set it up easily using docker and [Ethbian
OS(opens in a new tab)](https://ethbian.org/index.html) for RPi 4.

In this tutorial, we'll set up your Geth client to push data to InfluxDB to
create a database and Grafana to create a graph visualisation of the data.
Doing it manually will help you understand the process better, alter it, and
deploy in different environments.

## Setting up InfluxDB

First, let's download and install InfluxDB. Various download options can be
found at [Influxdata release page(opens in a new
tab)](https://portal.influxdata.com/downloads/). Pick the one that suits your
environment. You can also install it from a [repository(opens in a new
tab)](https://repos.influxdata.com/). For example in Debian based
distribution:

    
    
    1curl -tlsv1.3 --proto =https -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add
    
    2source /etc/lsb-release
    
    3echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
    
    4sudo apt update
    
    5sudo apt install influxdb -y
    
    6sudo systemctl enable influxdb
    
    7sudo systemctl start influxdb
    
    8sudo apt install influxdb-client

After successfully installing InfluxDB, make sure it's running on background.
By default, it is reachable at `localhost:8086`. Before using `influx` client,
you have to create new user with admin privileges. This user will serve for
high level management, creating databases and users.

    
    
    1curl -XPOST "http://localhost:8086/query" --data-urlencode "q=CREATE USER username WITH PASSWORD 'password' WITH ALL PRIVILEGES"

Now you can use influx client to enter [InfluxDB shell(opens in a new
tab)](https://docs.influxdata.com/influxdb/v1.8/tools/shell/) with this user.

    
    
    1influx -username 'username' -password 'password'

Directly communicating with InfluxDB in its shell, you can create database and
user for geth metrics.

    
    
    1create database geth
    
    2create user geth with password choosepassword

Verify created entries with:

    
    
    1show databases
    
    2show users

Leave InfluxDB shell.

    
    
    1exit

InfluxDB is running and configured to store metrics from Geth.

## Preparing Geth

After setting up database, we need to enable metrics collection in Geth. Pay
attention to `METRICS AND STATS OPTIONS` in `geth --help`. Multiple options
can be found there, in this case we want Geth to push data into InfluxDB.
Basic setup specifies endpoint where InfluxDB is reachable and authentication
for the database.

    
    
    1geth --metrics --metrics.influxdb --metrics.influxdb.endpoint "http://0.0.0.0:8086" --metrics.influxdb.username "geth" --metrics.influxdb.password "chosenpassword"

This flags can be appended to a command starting the client or saved to the
configuration file.

You can verify that Geth is successfully pushing data, for instance by listing
metrics in database. In InfluxDB shell:

    
    
    1use geth
    
    2show measurements

## Setting up Grafana

Next step is installing Grafana which will interpret data graphically. Follow
installation process for your environment in Grafana documentation. Make sure
to install OSS version if you don't want otherwise. Example installation steps
for Debian distributions using repository:

    
    
    1curl -tlsv1.3 --proto =https -sL https://packages.grafana.com/gpg.key | sudo apt-key add -
    
    2echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
    
    3sudo apt update
    
    4sudo apt install grafana
    
    5sudo systemctl enable grafana-server
    
    6sudo systemctl start grafana-server

When you've got Grafana running, it should be reachable at `localhost:3000`.
Use your preferred browser to access this path, then login with the default
credentials (user: `admin` and password: `admin`). When prompted, change the
default password and save.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana1.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana1.png)

You will be redirected to the Grafana home page. First, set up your source
data. Click on the configuration icon in the left bar and select "Data
sources".

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana2.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana2.png)

There aren't any data sources created yet, click on "Add data source" to
define one.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana3.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana3.png)

For this setup, select "InfluxDB" and proceed.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana4.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana4.png)

Data source configuration is pretty straight forward if you are running tools
on the same machine. You need to set the InfluxDB address and details for
accessing the database. Refer to the picture below.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana5.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana5.png)

If everything is complete and InfluxDB is reachable, click on "Save and test"
and wait for the confirmation to pop up.

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana6.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana6.png)

Grafana is now set up to read data from InfluxDB. Now you need to create a
dashboard which will interpret and display it. Dashboards properties are
encoded in JSON files which can be created by anybody and easily imported. On
the left bar, click on "Create and Import".

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana7.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana7.png)

For a Geth monitoring dashboard, copy the ID of [this dashboard(opens in a new
tab)](https://grafana.com/grafana/dashboards/13877/) and paste it in the
"Import page" in Grafana. After saving the dashboard, it should look like
this:

[![](/_next/image/?url=%2Fcontent%2Fdevelopers%2Ftutorials%2Fmonitoring-geth-
with-influxdb-and-
grafana%2Fgrafana8.png&w=1920&q=75)](/content/developers/tutorials/monitoring-
geth-with-influxdb-and-grafana/grafana8.png)

You can modify your dashboards. Each panel can be edited, moved, removed or
added. You can change your configurations. It's up to you! To learn more about
how dashboards work, refer to [Grafana's documentation(opens in a new
tab)](https://grafana.com/docs/grafana/latest/dashboards/). You might also be
interested in [Alerting(opens in a new
tab)](https://grafana.com/docs/grafana/latest/alerting/). This lets you set up
alert notifications for when metrics reach certain values. Various
communication channels are supported.

n

Last edit: [@nhsz(opens in a new tab)](https://github.com/nhsz), August 15,
2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/monitoring-geth-with-influxdb-and-grafana/index.md)
  * On this page

    * Prerequisites
    * Monitoring stack
    * Setting up InfluxDB
    * Preparing Geth
    * Setting up Grafana

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

