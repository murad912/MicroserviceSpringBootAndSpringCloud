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
---------------------------------------------------------------------------------------------------------------------------------------
                                 Liquebase configuration (db.changelog-1.0.xml
<?xml version="1.0" encoding="UTF-8"?>

<databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.0.xsd
        http://www.liquibase.org/xml/ns/dbchangelog-ext http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">

    <changeSet id="1" author="senol">
        <sql>
            CREATE TABLE user (
            id BIGINT NOT NULL AUTO_INCREMENT,
            username VARCHAR(255) NOT NULL,
            password VARCHAR(255) NOT NULL,
            name VARCHAR(255) NOT NULL,
            role VARCHAR(10) NOT NULL,
            CONSTRAINT pk_id PRIMARY KEY (id)
            );
        </sql>
        <rollback>
            DROP TABLE user;
        </rollback>
    </changeSet>

    <changeSet id="2" author="senol">
        <sql>
            ALTER TABLE user ADD email varchar(255);
        </sql>
        <rollback>
            ALTER TABLE user DROP COLUMN email;
        </rollback>
    </changeSet>
</databaseChangeLog>

