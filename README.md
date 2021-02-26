"# MicroserviceSpringBootAndSpringCloud" 


1. User-Manager-Service

   ->JPA
   ->Lombox
   ->MYSQL 
   ->REST 
   ->Eureka
   -----------------------------------------------------------------------------------------------------------------------------------------
* Application.property configuration
*server.port=8000
spring.application.name=user-service
spring.datasource.url=jdbc:mysql://localhost:3306/micro_user?useUnicode=true&useLegacyDatetimeCode=false&serverTimezone=UTC&createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=falsespring.datasource.url=jdbc:mysql://localhost:3306/micro_user?useUnicode=true&useLegacyDatetimeCode=false&serverTimezone=UTC&createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false
spring.datasource.username=root
spring.datasource.password=admin
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver


#none,create,update,validate
spring.jpa.hibernate.ddl-auto=none

#liquibase
spring.liquibase.change-log=classpath:/db/changelog/db.changelog-master.xml
--------------------------------------------------------------------------------------------------------------------------------------------------
                              User.class
package com.mur.microserviceusermanagement.model;

import lombok.Data;

import lombok.Data;

import javax.persistence.*;

@Data
@Entity
@Table(name = "user")
public class User {

    @Id
    //Generation Types:
    //Auto: Default one. It does not take any specific action.
    //Identity: Auto increment.
    //Sequence: Oracle or Posgresql creates variable to auto increment.
    //Table: Hibernate uses a database table to simulate a sequence.
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    @Enumerated(value = EnumType.STRING)
    @Column(name = "role")
    private Role role;
}
-----------------------------------------------------------------------------------------------------------------------------------
                           Role.class
package com.mur.microserviceusermanagement.model;

public enum Role {
    USER,
    ADMIN
}

