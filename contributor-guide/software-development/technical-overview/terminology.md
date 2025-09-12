# Terminology

While we strive as a team to use language that is inclusive to newcomers, there will inevitably be scenarios where we have to use terms that may not be immediately understood by anyone less familiar with the application. In an effort to bridge that gap, the following is a list of technical terms that are frequently used within the context of the OpenBoxes application:

* **Controller**: Files under `/grails-app/controllers` . The entrypoints for backend APIs.
* **Service**: Files under `/grails-app/services` . Classes that hold the main business logic for out APIs.
* **Domain/Entity**: Files under `/grails-app/domain` . The Groovy representation of our database entities. We use GORM-generated methods on these entities to query the database. For example: `Product.list()`
