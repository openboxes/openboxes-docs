# Our Tech Stack

The following is an overview of the technologies that we use to build and run the OpenBoxes application.

### Frontend

* [React](https://react.dev/): Our current frontend framework.
* [Groovy Server Pages](https://gsp.grails.org/latest/guide/index.html) (GSPs): A Grails technology that functions similarly to Java/Jakarta Server Pages (JSPs). For creating dynamically generated HTML. We use this as our frontend for our old features. It has since been replaced by React for all new features.



### Backend

* [Grails](https://grails.apache.org/): Our backend framework. Written in [Groovy](https://groovy-lang.org/). Is a wrapper on the [SpringBoot](https://spring.io/projects/spring-boot) framework.
* [Apache Tomcat](https://tomcat.apache.org/): The Servlet container that we wrap OpenBoxes with to make it a proper HTTP request handler.
* [Quartz](https://www.quartz-scheduler.org/): A job scheduling library. Allows us to set up crons / scheduled tasks that run on regular intervals. We typically use these Quartz jobs as data cleanup / synchronization mechanisms such as refreshing product availability.
* [Gradle](https://gradle.org/): A build automation / dependency management tool. Automate the compilation and packaging of the application.



### Database

* [MySQL](https://www.mysql.com/) / [MariaDB](https://mariadb.org/): The relational database that stores all OpenBoxes data. If given a choice, we recommend MariaDB
* [GORM](https://gorm.grails.org/): Grails Object Relational Mapping. A data source framework used by Grails that allows us to query the database via Groovy method calls on Domain objects. This means that we can query the datbase without using language-specific queries. This masks the underlying database from the application itself, which allows us to support multiple different SQL server implementations (MySQL, MariaDB...). We use GORM-for-[Hiberate](https://hibernate.org/orm/) since we use a SQL-based relational database.
* [Liquibase](https://www.liquibase.com/): Automates database migrations / schema changes via `changelog.groovy` files. See  the `/grails-app/migrations` folder for more information.



### Observability

* [Sentry](https://sentry.io/welcome/): Error monitoring and reporting as well as performance tracing.
* [New Relic](https://newrelic.com/): Provides a massive suite of observability tools. We primarily use it for log reporting / request tracing, and for system health monitoring

