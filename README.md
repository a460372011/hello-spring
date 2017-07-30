# 编写一个spring应用
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
## 1. 在项目里添加一个/src/main/webapp目录，然后添加一个WEB-INF文件夹，添加一个web.xml，修改pom里的packaging为war

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
</web-app>
```

## 2. 在web.xml文件里添加一个servlet，一个servletmapping
```
<servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/applicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>*.do</url-pattern>
 </servlet-mapping>
```
## 3. 在pom.xml里引入mvc模块：
```
     <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>4.3.10.RELEASE</version>
        </dependency>
```
## 4. 编写一个控制器，注解@Controller，使用@RequestMapping绑定url，使用@ResponseBody作为json视图，如果没有指定默认会跳转到内部视图

```
@Controller
@RequestMapping("/rootpath")
public class MyController {
    @ResponseBody
    @RequestMapping("/b")
    public MyUser hello(){
        MyUser m = new MyUser();
        m.setAge(10);
        m.setName("abc");
        return m;
    }

    @RequestMapping("/a")
    public String helloabc(){
        return "abc";
    }
}
```
## 5。 运行程序，pom里添加插件jetty-maven-plugin，使用jetty:run运行
```
<build>
        <plugins>
            <plugin>
                <groupId>org.eclipse.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <version>9.4.6.v20170531</version>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <webApp>
                        <contextPath>/</contextPath>
                    </webApp>
                </configuration>
            </plugin>
        </plugins>
</build>
```
