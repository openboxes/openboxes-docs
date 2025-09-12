# Running OpenBoxes Locally

### Installation Instructions

The following instructions describe the minimum steps required to build and run the application on your local machine.

If you're system administrator looking to deploy the application to a production server, you'll want to read through the [installation documentation](http://docs.openboxes.com/en/latest/installation/) instead.

#### 1. Install Dependencies

Each of the following will need to be installed on your local machine:

| Dependency                                                                                | Version                                                                                           |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [MariaDB](https://mariadb.com/kb/en/mariadb-10-11-4-release-notes/)                       | 10.11.4 ([MySQL 8.0](https://downloads.mysql.com/archives/community/) is a supported alternative) |
| NPM                                                                                       | 6.14.6                                                                                            |
| [Node.js](https://nodejs.org/en/download)                                                 | 14+                                                                                               |
| [Java](https://www.oracle.com/pl/java/technologies/javase/javase8-archive-downloads.html) | 8.0                                                                                               |
| [Grails](https://grails.org/download.html)                                                | 3.3.18                                                                                            |

**Installing Java and Grails**

We recommend using [SDK Man](https://sdkman.io/install) to easily install and manage your SDK versions. With it, you can install Java and Grails on the command line using:

```
sdk install java 8.0.452-zulu
sdk install grails 3.3.18
```

**Installing MariaDB (or MySQL)**

{% tabs %}
{% tab title="Linux" %}
You can install the SQL server via Advanced Package Tool:

```
sudo apt install mariadb-server-10.11.4
```

Or for MySQL:

```
sudo apt install mysql-server-8.0
```
{% endtab %}

{% tab title="Mac" %}
The easiest way to install a compatible database is by using [`brew install mariadb`](https://mariadb.com/kb/en/installing-mariadb-on-macos-using-homebrew/).

Alternatively, ARM builds of MySQL 8 are available. Consider downloading [8.x LTS here](https://dev.mysql.com/downloads/mysql/).
{% endtab %}
{% endtabs %}

**Installing NPM and Node**

{% tabs %}
{% tab title="Linux" %}
You can install the Node and NPM via Advanced Package Tool:

<pre><code><strong>sudo apt install nodejs
</strong>sudo apt install npm=6.14.6
</code></pre>
{% endtab %}

{% tab title="Mac" %}
There is no ARM build of Node 14 but you can run it via x86 emulation as follows:

1. `/usr/sbin/softwareupdate --install-rosetta --agree-to-license`
2. Install `nvm` (_only_ – do _not_ install `node` itself) using [these instructions](https://nodejs.org/en/download)
3. Launch a terminal that uses Rosetta to pretend to be an x86 host: `arch -x86_64 bash`
4. Within that terminal, run `nvm install 14`
5. Open up a new terminal and run the following command; you should see an `x86_64` binary, which should be able to run successfully on an ARM host.

```bash
$ hash -r && type node | awk '{print $3}' | xargs file
\*\*/.nvm/versions/node/v14.21.3/bin/node: Mach-O 64-bit executable x86_64
$ arch; node --version
arm64
v14.21.3
```
{% endtab %}
{% endtabs %}

#### 2. Configure the database instance

Create the openboxes database:

```
mysql -u root -p -e 'create database openboxes default charset utf8;'
```

Create the "openboxes" user:

```
mysql -u root -p -e 'CREATE USER "openboxes"@"localhost" IDENTIFIED BY "openboxes";'
mysql -u root -p -e 'GRANT ALL PRIVILEGES ON openboxes.* TO "openboxes"@"localhost";'
mysql -u root -p -e 'FLUSH PRIVILEGES;'
```

#### 3. Create Openboxes configuration file

Create the `~/.grails/openboxes.yml` file with the following contents:

{% tabs %}
{% tab title="MariaDB" %}
```
dataSource.url=jdbc:mariadb://localhost:3306/openboxes?serverTimezone=UTC&useSSL=false
dataSource.driverClassName: org.mariadb.jdbc.Driver
```
{% endtab %}

{% tab title="MySQL" %}
No custom config is required. Move on to the next step.
{% endtab %}
{% endtabs %}

#### 4. Install NPM dependencies

If you haven't already, clone the repository, then cd to the main folder of the project and run:

```
npm config set engine-strict true
npm install
```

#### 5. Start the application

```
grails run-app
```

This will start the application in development mode using an internal Tomcat instance. This will also build all the remaining dependencies for the project. You may need to run the `grails compile` command beforehand, or run `grails run-app` several times in order to download all dependencies.

#### 6. Log into OpenBoxes

Navigate to `http://localhost:8080/openboxes` and log in as an admin using the default credentials (username: `admin` and password: `password`). From there, you can create further accounts as needed.



### **Tips and tricks**

#### **Disable Background Jobs**

There are many different background jobs that are periodically executed while the application server is running. Some of the jobs are ran every minute. This is slow, and can be quite resource intensive, so unless you need a job to be running, we recommend that you disable them when running the app locally.

To disable the jobs, add the following to your openboxes.yml:

```
# This stops the background jobs from running on app startup,
# which is very resource intensive and slow.
openboxes:
  refreshAnalyticsDataOnStartup.enabled: false

  jobs:
    # If you're not modifying stock you can disable this, otherwise keep it enabled
    refreshProductAvailabilityJob.enabled: true
    
    sendStockAlertsJob.enabled: false
    refreshInventorySnapshotJob.enabled: false
    refreshInventorySnapshotAfterTransactionJob.enabled: false
    refreshOrderSummaryJob.enabled: false
    refreshTransactionFactJob.enabled: false
    refreshStockoutDataJob.enabled: false
    refreshDemandDataJob.enabled: false
    assignIdentifierJob.enabled: false
    calculateHistoricalQuantityJob.enabled: false
    dataCleaningJob.enabled: false
    dataMigrationJob.enabled: false
    updateExchangeRatesJob.enabled: false
```



#### **Enable React Hot-Reloading**

If you're doing development on the React frontend, you'll likely find it useful to run the frontend in hot-swap mode.

In addition to running the regular application server (via the `grails run-app` command) run the following command in a separate command-line process:

```
npm run watch
```

This will cause the fronted to rebuild itself automatically after any code change that you make. All you need to do is refresh the browser window to see the changes take effect. Without this line, you'd need to restart your server to have any React changes take effect.

In addition to this, now that you're building the frontend NPM dependencies yourself, you can comment out any lines in the `build.gradle` file that contain `dependsOn 'npm_run_bundle'.` This allows the backend to start much faster since it prevents it from also rebuilding the NPM depedencies.

