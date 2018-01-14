---
layout: wiki
title: Hibernate
toc: true
---

### 개요
객체지향프로그래밍(OOP, Object Oriented Programming)은 우리에게 너무나도 익숙한 개념이 되었다. (물론 프로그래머들에게는...) 그런데 프로그램이 아닌 데이터베이스의 세계로 가보면 객체지향 데이터베이스는 지고 지금의 DBMS 시장은 관계형 데이터베이스(RDB, Relational DataBase)가 패권을 차지한 상태이다.

그런데 우리가 JDBC와 같은 프로그래밍을 하게 되면 이 두개의 다른 개념에서 오는 차이를 극복해야 하는 순간이 발생한다. 물론 대부분의 프로그래머들은 그러한 차이를 인식하지도 못하고 넘어가는 경우가 태반이지만, 실제로 이러한 두 개념의 차이를 극복하기 위해 애쓰는 사람들이 존재한다. 그리하여 나온 개념이 바로 객체-관계형 매핑(ORM, Object-Relation Mapping)이다. Sun의 JDO와 아파치 그룹의 OJB와 같은 것이 그 예인데, Hibernate는 그러한 ORM을 구현한 프레임워크 중에 가장 유명한 프레임워크이다.

### 기본 설정
다음은 Hibernate의 기본 설정파일인 'hibernate.cfg.xml'의 예이다.

```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
       "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
       "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
    <session-factory>
        <!-- Database connection settings -->
        <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="connection.url">
        jdbc:mysql://localhost/test?useUnicode=true&amp;characterEncoding=euckr
    </property>
        <property name="connection.username">root</property>
        <property name="connection.password">root</property>

        <!-- JDBC connection pool (use the built-in) -->
        <property name="connection.pool_size">1</property>

        <!-- SQL dialect -->
        <property name="dialect">org.hibernate.dialect.MySQLInnoDBDialect</property>

        <!-- Enable Hibernate's automatic session context management -->
        <property name="current_session_context_class">thread</property>

        <!-- Disable the second-level cache  -->
        <property name="cache.provider_class">org.hibernate.cache.NoCacheProvider</property>

        <!-- Echo all executed SQL to stdout -->
        <property name="show_sql">true</property>

        <!-- Drop and re-create the database schema on startup -->
        <!--
           <property name="hbm2ddl.auto">create</property>
           <property name="hbm2ddl.auto">validate</property>
       -->
        <mapping resource="com/multicampus/c02/product/Mapping.hbm.xml"/>
    </session-factory>
</hibernate-configuration>
```

Optional configuration properties: <http://docs.jboss.org/hibernate/core/3.3/reference/en/html/session-configuration.html>

#### List of Hibernate SQL Dialects|

|RDBMS|Dialect|
|-----|-------|
|DB2|org.hibernate.dialect.DB2Dialect|
|DB2 AS/400|org.hibernate.dialect.DB2400Dialect|
|DB2 OS390|org.hibernate.dialect.DB2390Dialect|
|PostgreSQL|org.hibernate.dialect.PostgreSQLDialect|
|MySQL|org.hibernate.dialect.MySQLDialect<br>org.hibernate.dialect.MySQL5Dialect|
|MySQL with InnoDB|org.hibernate.dialect.MySQLInnoDBDialect<br>org.hibernate.dialect.MySQL5InnoDBDialect|
|MySQL with MyISAM|org.hibernate.dialect.MySQLMyISAMDialect<br>org.hibernate.dialect.MySQL5MyISAMDialect|
|Oracle (any version)|org.hibernate.dialect.OracleDialect|
|Oracle 9i/10g|org.hibernate.dialect.Oracle9Dialect|
|Sybase|org.hibernate.dialect.SybaseDialect|
|Sybase Anywhere|org.hibernate.dialect.SybaseAnywhereDialect|
|Microsoft SQL Server|org.hibernate.dialect.SQLServerDialect|
|SAP DB|org.hibernate.dialect.SAPDBDialect|
|Informix|org.hibernate.dialect.InformixDialect|
|HypersonicSQL|org.hibernate.dialect.HSQLDialect|
|Ingres|org.hibernate.dialect.IngresDialect|
|Progress|org.hibernate.dialect.ProgressDialect|
|Mckoi SQL|org.hibernate.dialect.MckoiDialect|
|Interbase|org.hibernate.dialect.InterbaseDialect|
|Pointbase|org.hibernate.dialect.PointbaseDialect|
|FrontBase|org.hibernate.dialect.FrontbaseDialect|
|Firebird|org.hibernate.dialect.FirebirdDialect|

### Hibernate Logger
Hibernate를 사용하게 되면 기본적으로 slf4j 로거가 사용된다. 아래 두 라이브러리가 classpath에 위치해야 하며, 기존 log4j와 함께 사용하면서 로그정책을 적용하기 위해서는 아래와 같은 기준을 사용한다.
* slf4j-api-1.6.1.jar
* slf4j-jdk14-1.6.1.jar

|Name|Description|
|----|-----------|
|hibernate.show_sql|Hibernate을 통해 생성된 SQL을 콘솔에 남길 것인지 여부를 정의하는 속성 (true,false)|
|hibernate.format_sql|hibernate.show_sql=true인 경우 해당 SQL문의 포맷을 정돈하여 콘솔에 남길 것인지 여부를 정의하는 속성 (true,false)|
|hibernate.use_sql_comments	|Hibernate을 통해 생성된 SQL을 콘솔에 남길 때 Comments도 같이 남길 것인지 여부를 정의하는 속성 (true,false)|

아래는 위에서 언급한 hibernate.show_sql, hibernate.format_sql 속성을 정의하였을 경우 Hibernate를 통해 생성된 SQL문의 예이다.

```sql
Hibernate: 
    INSERT 
    INTO
        PUBLIC.COUNTRY
        (COUNTRY_ID, COUNTRY_NAME, COUNTRY_CODE) 
    VALUES
        (?, ?, ?)
```

#### Logger Categories

|Category|Function|번역|
|--------|--------|----|
|org.hibernate|Log everything (a lot of information, but very useful for troubleshooting)|전부 Logging|
|org.hibernate.SQL|Log all SQL DML statements as they are executed|실행되는 모든 DML 쿼리 Logging|
|org.hibernate.type|Log all JDBC parameters|모든 JDBC 인자 Logging|
|org.hibernate.tool.hbm2ddl|Log all SQL DDL statements as they are executed|실행되는 모든 DDL 쿼리 Logging|
|org.hibernate.pretty|Log the state of all entities (max 20 entities) associated with the session at flush time|Flush 수행시 세션에 저장된 모든 개체(최대 20개)의 상태를 Logging|
|org.hibernate.cache|Log all second-level cache activity|2nd Level Cache 수행 내역을 Logging|
|org.hibernate.transaction|Log transaction related activity|트랜잭션 수행 내역을 Logging|
|org.hibernate.jdbc|Log all JDBC resource acquisition|모든 JDBC 자원 요청을 Logging|
|org.hibernate.hql.ast.AST|Log HQL and SQL ASTs during query parsing|쿼리를 파싱하는 동안 HQL과 SQL AST를 Logging|
|org.hibernate.secure|Log all JAAS authorization requests|모든 JAAS 인증 요청을 Logging|

### Hibernate Shard

Hibernate는 Shard를 지원(http://www.hibernate.org/subprojects/shards.html)한다. 그런데 문제는 여기서 제시하는 샘플은 기본적인 Hibernate의 SessionFactory를 생성하여 Shard를 구현한 것으로 Spring IOC를 이용하고자 할 때에는 문제가 있다. 따라서 아래와 같은 Custom 클래스를 작성하여 Spring으로 ShardedSessionFactory를 생성해보자.

아래 샘플 외에도 아마존 문서(<http://aws.amazon.com/articles/0040302286264415?_encoding=UTF8&queryArg=searchQuery&x=0&fromSearch=1&y=0&searchPath=all&searchQuery=shard>)에도 잘 정리되어 있다.

#### Spring Bean SessionFactory
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:tx="http://www.springframework.org/schema/tx"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
                                                http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
                                                http://www.springframework.org/schema/tx
                                                http://www.springframework.org/schema/tx/spring-tx-2.5.xsd">

        <!-- A Hibernate SessionFactory for mapping Accounts and Restaurants from object to relation tables -->
        <bean id="shardedSessionFactoryBean" class="com.project.hibernate.shard.ShardedSessionFactoryBean">
                <property name="annotatedClasses">
                        <list>
                                <value>com.project.hibernate.service.vo.WeatherReport</value>
                        </list>
                </property>
                <property name="hibernateConfigurations">
                        <list>
                                <value>hibernate/shard0.hibernate.cfg.xml</value>
                                <value>hibernate/shard1.hibernate.cfg.xml</value>
                        </list>
                </property>
        </bean>
        <bean id="sessionFactory" factory-bean="shardedSessionFactoryBean"
                factory-method="createSessionFactory">
        </bean>
</beans>
```

#### ShardedSessionFactoryBean
```java
@SuppressWarnings("rawtypes")
public class ShardedSessionFactoryBean {

        private List<Class> annotatedClasses;
        private List<String> hibernateConfigurations;

        public void setAnnotatedClasses(List<Class> annotatedClasses) {
                this.annotatedClasses = annotatedClasses;
        }

        public void setHibernateConfigurations(List<String> hibernateConfigurations) {
                this.hibernateConfigurations = hibernateConfigurations;
        }

        public SessionFactory createSessionFactory() {
                Configuration prototypeConfig = this.getPrototypeConfig(this.hibernateConfigurations.get(0), this.annotatedClasses);

                List<ShardConfiguration> shardConfigs = new ArrayList<ShardConfiguration>();
                for (String hibconfig : this.hibernateConfigurations) {
                        shardConfigs.add(buildShardConfig(hibconfig));
                }

                ShardStrategyFactory shardStrategyFactory = buildShardStrategyFactory();
                ShardedConfiguration shardedConfig = new ShardedConfiguration(prototypeConfig, shardConfigs, shardStrategyFactory);
                return shardedConfig.buildShardedSessionFactory();
        }

        private Configuration getPrototypeConfig(String hibernateFile, List<Class> annotatedClasses) {
                Configuration prototypeConfig = this.getConfiguration(hibernateFile);
                for (Class cls : annotatedClasses) {
                        prototypeConfig.addAnnotatedClass(cls);
                }
                return prototypeConfig;
        }

        private Configuration getConfiguration(String file) {
                return new Configuration().configure(file);
        }

        private ShardStrategyFactory buildShardStrategyFactory() {
                ShardStrategyFactory shardStrategyFactory = new ShardStrategyFactory() {
                        public ShardStrategy newShardStrategy(List<ShardId> shardIds) {
                                RoundRobinShardLoadBalancer loadBalancer = new RoundRobinShardLoadBalancer(shardIds);
                                ShardSelectionStrategy pss = new RoundRobinShardSelectionStrategy(loadBalancer);
                                ShardResolutionStrategy prs = new AllShardsShardResolutionStrategy(shardIds);
                                ShardAccessStrategy pas = new SequentialShardAccessStrategy();
                                return new ShardStrategyImpl(pss, prs, pas);
                        }
                };
                return shardStrategyFactory;
        }

        private ShardConfiguration buildShardConfig(String configFile) {
                Configuration config = new Configuration().configure(configFile);
                return new ConfigurationToShardConfigurationAdapter(config);
        }

}
```

#### Annotation VO @id Generator
```java
@Entity
@Table(name = "WEATHER_REPORT")
public class WeatherReport implements Serializable {
        @Id
        @GeneratedValue(generator = "WeatherReportIdGenerator")
        @GenericGenerator(name = "WeatherReportIdGenerator", strategy = "org.hibernate.shards.id.ShardedTableHiLoGenerator")
        @Column(name = "REPORT_ID")
        private Integer reportId;

        @Column(name = "CONTINENT")
        private String continent;

        @Column(name = "LATITUDE")
        private BigDecimal latitude;

        @Column(name = "LONGITUDE")
        private BigDecimal longitude;

        @Column(name = "TEMPERATURE")
        private int temperature;

        @Temporal(TemporalType.TIMESTAMP)
        @Column(name = "REPORT_TIME")
        private Date reportTime;

        @Lob
        @Column(name = "PICTURE")
        private byte[] picture;

        @OneToMany(cascade = CascadeType.ALL)
        @JoinColumn(name = "REPORT_ID")
        private Set<WeatherReportVer> versions = new HashSet<WeatherReportVer>();

        // gettes and setters
}

@Entity
@Table(name = "WEATHER_REPORT_VER")
public class WeatherReportVer implements Serializable {
        @Id
        @GeneratedValue(generator = "WeatherReportVerIdGenerator")
        @GenericGenerator(name = "WeatherReportVerIdGenerator", strategy = "org.hibernate.shards.id.ShardedTableHiLoGenerator")
        @Column(name = "REPORT_VER_ID")
        private Integer reportVerId;

        @Column(name = "VERSION")
        private BigDecimal version;

        @Column(name = "AUTHOR")
        private String author;

        // gettes and setters
}
```

#### Table Sample
```sql
CREATE TABLE WEATHER_REPORT (
    REPORT_ID INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    CONTINENT ENUM('AFRICA', 'ANTARCTICA', 'ASIA', 'AUSTRALIA', 'EUROPE', 'NORTH AMERICA', 'SOUTH AMERICA'),
    LATITUDE FLOAT,
    LONGITUDE FLOAT,
    TEMPERATURE INT,
    PICTURE BLOB,
    REPORT_TIME TIMESTAMP
);

CREATE TABLE WEATHER_REPORT_VER (
    REPORT_VER_ID INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    AUTHOR VARCHAR,
    VERSION FLOAT,
    REPORT_ID CONSTRAINT FOREIGN KEY REFERENCES WEATHER_REPORT(REPORT_ID)
);
```
