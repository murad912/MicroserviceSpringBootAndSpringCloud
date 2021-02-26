"# MicroserviceSpringBootAndSpringCloud" 


1. User-Manager-Service

   ->JPA
   ->Lombox
   ->MYSQL 
   ->REST 
   ->Eureka
* Application.property configuration
       server.port=8000
      spring.application.name=user-service
      spring.datasource.url=jdbc:mysql://localhost:3306/micro_user?               useUnicode=true&useLegacyDatetimeCode=false&serverTimezone=UTC&createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=falsespring.datasource.url=jdbc:mysql://localhost:3306/micro_user?useUnicode=true&useLegacyDatetimeCode=false&serverTimezone=UTC&createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false
      spring.datasource.username=root
      spring.datasource.password=admin
      spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver


      #none,create,update,validate
      spring.jpa.hibernate.ddl-auto=none

      #liquibase
      spring.liquibase.change-log=classpath:/db/changelog/db.changelog-master.xml
* Hibernet 

