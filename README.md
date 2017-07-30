## 编写一个spring应用
### 1. 创建maven项目，pom.xml里添加maven引用

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.10.RELEASE</version>
    </dependency>
</dependencies>
```
### 2. 创建一个spring配置文件myspring.xml
### 3. 创建一个Bean类，提供一些public方法，在spring配置文件里定义

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myBeanId" class="com.kavy.spring.hellospring.BeanA"></bean>
</beans>
```

### 4. 创建一个启动类，并使用ClassPathXmlApplicationContext加载配置类启动容器

```
public class AppMain {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("myspring.xml");
        BeanA a = context.getBean("myBeanId",BeanA.class);
        a.hello();
    }
}
```


# 编写一个web应用
## 1. 在项目里添加一个web目录，然后添加一个WEB-INF文件夹，添加一个web.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
</web-app>
```



