# [![Mattermost](https://user-images.githubusercontent.com/7205829/137170381-fe86eef0-bccc-4fdd-8e92-b258884ebdd7.png)](https://mattermost.com)

[Mattermost](https://mattermost.com) is an open source platform for secure collaboration across the entire software development lifecycle. This repo is the primary source for core development on the Mattermost platform; it's written in Go and React and runs as a single Linux binary with MySQL or PostgreSQL. A new compiled version is released under an MIT license every month on the 16th.

[Use it for free in Mattermost Cloud](https://mattermost.com/sign-up/?utm_source=github-mattermost-server-readme) or [deploy on-premises](https://mattermost.com/deploy/?utm_source=github-mattermost-server-readme).

<img width="1006" alt="mattermost-hero" src="https://user-images.githubusercontent.com/7205829/136107976-7a894c9e-290a-490d-8501-e5fdbfc3785a.png">

Learn more about the following use cases with Mattermost:

- [DevSecOps](https://mattermost.com/solutions/use-cases/devops/?utm_source=github-mattermost-server-readme)
- [Incident Resolution](https://mattermost.com/solutions/use-cases/incident-resolution/?utm_source=github-mattermost-server-readme)
- [IT Service Desk](https://mattermost.com/solutions/use-cases/it-service-desk/?utm_source=github-mattermost-server-readme)

Other useful resources:

- [Download and Install Mattermost](https://docs.mattermost.com/guides/deployment.html) - Install, setup, and configure your own Mattermost instance.
- [Product documentation](https://docs.mattermost.com/) - Learn how to run a Mattermost instance and take advantage of all the features.
- [Developer documentation](https://developers.mattermost.com/) - Contribute code to Mattermost or build an integration via APIs, Webhooks, slash commands, Apps, and plugins.

Table of contents
=================

  * [Try out Mattermost](#try-out-mattermost)
  * [Install Mattermost Server](#install-mattermost-application)
  * [Install Mattermost](#install-mattermost-application)
  * [Native Mobile and Desktop Apps](#native-mobile-and-desktop-apps)
  * [Get Security Bulletins](#get-security-bulletins)
  * [Get Involved](#get-involved)
  * [Learn More](#learn-more)
  * [Get the Latest News](#get-the-latest-news)
  * [Contributing](#contributing)

## Install Mattermost Server (Go)
### Dependencies
1. [Docker v17.12.0+](https://docs.docker.com/desktop/install/mac-install/)
2. [Docker Compose v1.21.0+](https://docs.docker.com/compose/)
3. [Go v1.18.0+](https://go.dev/dl/)
    - If you are on a Mac and have brew installed you can use the following command to install Go: `brew install go`

### Configuring Docker
1. Backup any existing containers:

```
mysqldump -h 127.0.0.1 --column-statistics=0 -u mmuser -p mattermost_test > mm_mysql_backup.sql
pg_dump -U mmuser -W -d mattermost_test -h 127.0.0.1 > mm_postgres_backup.bak
```

2. Upgrade and starting new docker-compose managed containers:

```
mysql -u mmuser -p -h 127.0.0.1 mattermost_test < mm_mysql_backup.sql
psql -U mmuser -W -h 127.0.0.1 -f mm_postgres_backup.bak mattermost_test
```

### Update Shell's Initialization Script
1. Find .basrc or .zshrc
    - You can check by doing `cd ~/` in the terminal
    - Then check if either file exists using `ls -a`
2. Update either file with `ulimit -n 8096`

### Fork and Clone the mattermost-server code
1. Go to https://github.com/mattermost/mattermost-server
2. Click on fork on the top right of the screen:

![image](https://user-images.githubusercontent.com/63694045/197295365-cfa46d28-93f2-4144-9674-e32bc52fca1b.png)

3. Create a fork for your account

![image](https://user-images.githubusercontent.com/63694045/197295959-c8f40663-301c-49be-af9e-664d2370c821.png)

4. In your terminal and find a place to clone your code
5. Clone your forked source: `git clone https://github.com/YOUR_GITHUB_USERNAME/mattermost-server.git`

### Starting and testing your server
1. To start your server, go to the location of your source code then:
    - `cd mattermost-server`
    - `make run-server`
2. To test your server, run the following in your terminal
    - `curl http://localhost:8065/api/v4/system/ping`
    - `make stop-server`
3. If successful, you will receive a JSON object from the curl command
4. To stop the server completely: `make stop-docker`

### Additional information/guides
[Link to Mattermost's online server guide](https://developers.mattermost.com/contribute/server/developer-setup) - Follow this guide if you want to write code for Mattermost.

## Install Mattermost Application

- [Download and Install Mattermost Self-Hosted](https://docs.mattermost.com/guides/deployment.html) - Deploy a Mattermost Self-hosted instance in minutes via Docker, Ubuntu, or tar.
- [Get started with Mattermost Cloud](https://customers.mattermost.com/cloud/signup) to use Mattermost instantly.

Other install guides:

- [Deploy Mattermost on Docker](https://docs.mattermost.com/install/install-docker.html)
- [Mattermost Omnibus](https://docs.mattermost.com/install/installing-mattermost-omnibus.html)
- [Install Mattermost from Tar](https://docs.mattermost.com/install/install-tar.html)
- [Ubuntu 20.04 LTS](https://docs.mattermost.com/install/installing-ubuntu-2004-LTS.html)
- [Kubernetes](https://docs.mattermost.com/install/install-kubernetes.html)
- [Helm](https://docs.mattermost.com/install/install-kubernetes.html#installing-the-operators-via-helm)
- [Debian Buster](https://docs.mattermost.com/install/install-debian.html)
- [RHEL 8](https://docs.mattermost.com/install/install-rhel-8.html)
- [More server install guides](https://docs.mattermost.com/guides/deployment.html)

## Native mobile and desktop apps

In addition to the web interface, you can also download Mattermost clients for [Android](https://mattermost.com/mattermost-android-app/), [iOS](https://mattermost.com/mattermost-ios-app/), [Windows PC](https://docs.mattermost.com/install/desktop-app-install.html#windows-10-windows-8-1), [macOS](https://docs.mattermost.com/install/desktop-app-install.html#macos-10-9), and [Linux](https://docs.mattermost.com/install/desktop-app-install.html#linux).

[![Google Play](https://user-images.githubusercontent.com/33878967/33095356-39b6fbf8-ceb8-11e7-8a61-c3a18fa5e658.png)](https://mattermost.com/mattermost-android-app/)  [![App Store](https://user-images.githubusercontent.com/33878967/33095353-397e69b4-ceb8-11e7-8175-f95a97d5274f.png)](https://itunes.apple.com/us/app/mattermost/id1257222717?mt=8)  [![Windows PC](https://user-images.githubusercontent.com/33878967/33095357-39cab8d2-ceb8-11e7-89a6-67dccc571ca3.png)](https://docs.mattermost.com/install/desktop.html#windows-10-windows-8-1-windows-7)  [![Mac OSX](https://user-images.githubusercontent.com/33878967/33095355-39a36f2a-ceb8-11e7-9b33-73d4f6d5d6c1.png)](https://docs.mattermost.com/install/desktop.html#macos-10-9)  [![Linux](https://user-images.githubusercontent.com/33878967/33095354-3990e256-ceb8-11e7-965d-b00a16e578de.png)](https://docs.mattermost.com/install/desktop.html#linux)

## Get security bulletins

Receive notifications of critical security updates. The sophistication of online attackers is perpetually increasing. If you're deploying Mattermost it's highly recommended you subscribe to the Mattermost Security Bulletin mailing list for updates on critical security releases.

[Subscribe here](https://mattermost.com/security-updates/#sign-up)

## Get involved

- [Contribute to Mattermost](https://handbook.mattermost.com/contributors/contributors/ways-to-contribute)
- [Find "Help Wanted" projects](https://github.com/mattermost/mattermost-server/issues?page=1&q=is%3Aissue+is%3Aopen+%22Help+Wanted%22&utf8=%E2%9C%93)
- [Join Developer Discussion on a Mattermost server for contributors](https://community.mattermost.com/signup_user_complete/?id=f1924a8db44ff3bb41c96424cdc20676)
- [Get Help With Mattermost](https://docs.mattermost.com/guides/get-help.html)

## Learn more

- [API options - webhooks, slash commands, drivers, and web service](https://api.mattermost.com/)
- [See who's using Mattermost](https://mattermost.com/customers/)
- [Browse over 700 Mattermost integrations](https://mattermost.com/marketplace/)

## License

See the [LICENSE file](LICENSE.txt) for license rights and limitations.

## Get the latest news

- **Twitter** - Follow [Mattermost](https://twitter.com/mattermost).
- **Blog** - Get the latest updates from the [Mattermost blog](https://mattermost.com/blog/).
- **Facebook** - Follow [Mattermost](https://www.facebook.com/MattermostHQ).
- **LinkedIn** - Follow [Mattermost](https://www.linkedin.com/company/mattermost/).
- **Email** - Subscribe to our [newsletter](https://mattermost.us11.list-manage.com/subscribe?u=6cdba22349ae374e188e7ab8e&id=2add1c8034) (1 or 2 per month).
- **Mattermost** - Join the ~contributors channel on [the Mattermost Community Server](https://community.mattermost.com). 
- **IRC** - Join the #matterbridge channel on [Freenode](https://freenode.net/) (thanks to [matterircd](https://github.com/42wim/matterircd)).

## Contributing

Please see [CONTRIBUTING.md](./CONTRIBUTING.md).
[Join the Mattermost Contributors server](https://community.mattermost.com/signup_user_complete/?id=codoy5s743rq5mk18i7u5ksz7e) to join community discussions about contributions, development, and more.
