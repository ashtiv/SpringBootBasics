## Spring Framework in 10 Steps

### Introduction

Spring Framework  is a widely used open-source application framework for building  enterprise Java  applications. It provides a comprehensive programming and  configuration model  for modern Java-based enterprise applications, making it popular in the industry due to its modular architecture, robustness, and flexibility.

### Spring Framework Levels

Spring Framework comprises three levels:

-   **Level 1**: Core Container - provides the fundamental functionality of the framework, including IoC (Inversion of Control) and DI (Dependency Injection).
-   **Level 2**: Data Access/Integration - provides support for  JDBC,  ORM  (Object-Relational Mapping), and other data access technologies.
-   **Level 3**: Web - provides support for building  web applications  using  Spring MVC  (Model-View-Controller) framework.

### Github Folder

The  Github folder  for this tutorial series contains all the necessary code examples for each step. You can access the  Github  folder by clicking  [here](https://github.com/in28minutes/spring-master-class/tree/master/01-spring-in-10-steps).

### Step 1 - Setting up a  Java Spring Project  using  [http://start.spring.io](http://start.spring.io/)

In Step 1, we will set up a new  Spring Boot project  using  [http://start.spring.io](http://start.spring.io/).  Spring Boot  is a popular project within the  Spring  ecosystem that provides an easier and faster way to set up a Spring-based application.

For example, let's say we want to build a simple  Spring Boot application  that exposes a  REST endpoint  to retrieve a list of students. We can follow these steps:

1.  Go to  [http://start.spring.io](http://start.spring.io/).
2.  Select the project type (Maven  or  Gradle), language (Java,  Kotlin, or  Groovy), and Spring Boot version.
3.  Choose any additional dependencies required for our project, such as Spring Web.
4.  Click on the Generate button to download the  project zip file.

### Step 2 - Understanding Tight Coupling using the  Binary Search Algorithm  Example

In Step 2, we will understand the concept of  tight coupling  using the  Binary Search Algorithm example. Tight coupling occurs when two or more components are dependent on each other, and any changes made to one component will affect the other.

For example, let's say we have two classes:  `BinarySearch`  and  `BubbleSort`. The  `BinarySearch`  class has a method  `search`  that performs a  binary search  on an array of integers. The  `BubbleSort`  class has a method  `sort`  that sorts an array of integers using the  bubble sort algorithm.

If we want to use the  `BinarySearch`  class to search a sorted array of integers, we need to first sort the array using the  `BubbleSort`  class. This creates a tight coupling between the two classes, as any changes made to the  `BubbleSort`  class will affect the  `BinarySearch`  class.

```
public class BinarySearch {
    public int search(int[] numbers, int numberToSearchFor) {
        BubbleSort bubbleSort = new BubbleSort();
        int[] sortedNumbers = bubbleSort.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

public class BubbleSort {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

```

### Step 3 - Making the Binary  Search Algorithm  Example Loosely Coupled

In Step 3, we will make the Binary Search Algorithm example loosely coupled by introducing an interface. An interface defines a set of methods that a class must implement. By using an interface, we can decouple the  `BinarySearch`  and  `BubbleSort`  classes.

For example, we can create an interface called  `SortAlgorithm`  that defines a single method  `sort`  that takes an array of integers as input and returns a sorted array of integers. The  `BubbleSort`  class will implement the  `SortAlgorithm`  interface, and the  `BinarySearch`  class will depend on the  `SortAlgorithm`  interface instead of the  `BubbleSort`  class.

This decouples the  `BinarySearch`  and  `BubbleSort`  classes, making them easier to maintain and modify.
```
public interface SortAlgorithm {
    int[] sort(int[] numbers);
}

public class BubbleSort implements SortAlgorithm {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

public class BinarySearch {
    private SortAlgorithm sortAlgorithm;

    public BinarySearch(SortAlgorithm sortAlgorithm) {
        this.sortAlgorithm = sortAlgorithm;
    }

    public int search(int[] numbers, int numberToSearchFor) {
        int[] sortedNumbers = sortAlgorithm.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

```

To use the updated code, we can create instances of the  `BubbleSort`  and  `BinarySearch`  classes as follows:
```
SortAlgorithm sortAlgorithm = new BubbleSort();
BinarySearch binarySearch = new BinarySearch(sortAlgorithm);
int[] numbers = {1, 2, 3, 4, 5};
int numberToSearchFor = 3;
int index = binarySearch.search(numbers, numberToSearchFor);
System.out.println("Number found at index: " + index);
```

### Step 4 - Using Spring Framework to Manage Dependencies - @Component, @Autowired

In Step 4, we will use the Spring Framework to manage dependencies using the  `@Component`  and  `@Autowired`  annotations. Spring Framework provides a powerful and flexible way to manage dependencies in a Java application.

For example, let's say we have a  `BinarySearchImpl`  class that implements the  `BinarySearch`  interface. The  `BinarySearchImpl`  class will depend on the  `SortAlgorithm`  interface, which will be injected into the class using the  `@Autowired`  annotation.

We can also annotate the  `BubbleSort`  class with the  `@Component`  annotation, which tells Spring Framework to create an instance of the  `BubbleSort`  class and manage its lifecycle.

By using the  `@Component`  and  `@Autowired`  annotations, we can easily manage the dependencies between the  `BinarySearchImpl`  and  `BubbleSort`  classes, making the application more modular and flexible.

## Conclusion

In this tutorial, we learned about the Spring Framework and its levels. We also covered the steps to set up a new Spring Boot project, understand tight coupling, make an example loosely coupled, and use Spring Framework to manage dependencies. Spring Framework is a powerful and popular  application framework  that provides a comprehensive programming and configuration model for modern Java-based enterprise applications.
## Step 4 - Using  Spring Framework  to Manage Dependencies -  `@Component`,  `@Autowired`

In Step 4, we use Spring Framework to manage dependencies between components in our Java application. Spring provides a number of annotations that we can use to define and inject dependencies between components, such as  `@Component`  and  `@Autowired`.

`@Component`  is an annotation that marks a  Java class  as a Spring-managed component. Spring will automatically create an instance of the component and manage its lifecycle. We can use the  `@Component`  annotation to define a component that implements the  `SortAlgorithm`  interface:

```
@Component
public class BubbleSort implements SortAlgorithm {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

```

`@Autowired`  is an annotation that tells Spring to inject a dependency into a Spring-managed component. We can use the  `@Autowired`  annotation to inject the  `SortAlgorithm`  implementation into the  `BinarySearch`  class:

```
@Component
public class BinarySearch {
    @Autowired
    private SortAlgorithm sortAlgorithm;

    public int search(int[] numbers, int numberToSearchFor) {
        int[] sortedNumbers = sortAlgorithm.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

```

By using  `@Component`  and  `@Autowired`, we can easily manage dependencies between components in our  Java  application and make our code more modular and maintainable.

## Step 5 - What is happening in the background?

In Step 5, we look at what is happening in the background when we use annotations like  `@Component`  and  `@Autowired`  in our Spring application.

When we use  `@Component`  to mark a class as a Spring-managed component, Spring will automatically create an instance of the component and manage its lifecycle. Spring maintains a context of all the components in our application, which allows it to manage dependencies between components and resolve  circular dependencies.

When we use  `@Autowired`  to inject dependencies into a component, Spring will look for a matching component in its context and inject it into the component. Spring uses a number of strategies to resolve dependencies, such as by type, by name, or by using  `@Qualifier`.

By understanding what is happening in the background when we use  Spring annotations, we can better manage dependencies in our application and troubleshoot issues that may arise.

## Example 
here's a simple example that shows how  `@Component`  and  `@Autowired`  annotations make  dependency injection  much simpler:
```
@Component
public class MyService {
  public void doSomething() {
    System.out.println("Doing something...");
  }
}

@Component
public class MyController {
  @Autowired
  private MyService myService;

  public void doSomethingInController() {
    myService.doSomething();
  }
}

```

In this example, we have a  `MyService`  class that does some work, and a  `MyController`  class that depends on  `MyService`. We mark both classes with  `@Component`  to indicate that they are Spring-managed beans.

We also use  `@Autowired`  annotation to inject an instance of  `MyService`  into  `myService`  field in  `MyController`.

Now, here's the same code without using  `@Component`  and  `@Autowired`  annotations:

```
public class MyService {
  public void doSomething() {
    System.out.println("Doing something...");
  }
}

public class MyController {
  private MyService myService;

  public MyController() {
    this.myService = new MyService();
  }

  public void doSomethingInController() {
    myService.doSomething();
  }
}

```

In this example, we manually create an instance of  `MyService`  in the constructor of  `MyController`  and assign it to  `myService`  field.

The problem with this approach is that it tightly couples  `MyController`  to  `MyService`. If we decide to change the implementation of  `MyService`  in the future, we would have to modify the constructor of  `MyController`  to use the new implementation.

Moreover, if we had multiple implementations of  `MyService`, we would have to manually instantiate the correct implementation in the constructor of  `MyController`. This can quickly become tedious and error-prone.

Using  `@Component`  and  `@Autowired`  annotations allows  Spring  to handle the instantiation and injection of dependencies automatically. This makes the code more flexible, maintainable, and easier to manage.
# Dynamic Auto Wiring and Troubleshooting - @Primary

In Spring Framework, we can use  `@Primary`  annotation to indicate that a particular bean should be given preference when multiple beans of the same type are candidates to be autowired by other components.

For example, let's say we have two implementations of a  service interface  `MyService`:
```
@Service
public class MyServiceImplOne implements MyService {
  // implementation
}

@Service
public class MyServiceImplTwo implements MyService {
  // implementation
}

```

Now, if we try to autowire  `MyService`  in another component, we'll get an exception because  Spring  doesn't know which implementation to use:
```
@Component
public class MyComponent {
  @Autowired
  private MyService myService; // throws NoUniqueBeanDefinitionException
}

```

To solve this problem, we can use  `@Primary`  annotation to indicate that one of the beans should be given preference:
```
@Service
@Primary
public class MyServiceImplOne implements MyService {
  // implementation
}

@Service
public class MyServiceImplTwo implements MyService {
  // implementation
}

```

Now, if we try to autowire  `MyService`  in another component, Spring will use  `MyServiceImplOne`  by default:
```
@Component
public class MyComponent {
  @Autowired
  private MyService myService; // uses MyServiceImplOne
}

```

# Fastest Approach to Solve All Your Exceptions

Exception handling  is an important part of any software application. Here are some tips to quickly solve exceptions:

1.  Read the Exception message: The first step in solving an  exception  is to read the exception message. The message will often give you a clue as to what went wrong.
    
2.  Check the Stack Trace: The  stack trace  will tell you where the exception occurred in your code. Look at the top of the stack trace to see the method that threw the exception.
    
3.  Google the Exception: Copy the exception message and search it on Google. You'll often find discussions on forums or  Stack Overflow  that can help you solve the problem.
    
4.  Check the Code: Look at the code that threw the exception and see if there are any obvious errors. Check for  null values,  incorrect variable types, and other common mistakes.
    
5.  Use a Debugger: If you still can't solve the problem, use a  debugger  to step through your code and see where the exception is occurring. This can help you pinpoint the problem.
    

By following these steps, you can quickly solve most exceptions and keep your application running smoothly.
## Step 7 - Spring Injection using Java Constructor and Setter Methods

Spring Framework  provides two main ways to inject dependencies into an object:  constructor injection  and  setter injection.

### Constructor Injection

Constructor injection involves passing the dependencies as arguments to the constructor of the object. Here's an example:

```
public class MyService {
    private final MyDependency myDependency;
    
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
    
    // ...
}

```

In this example, the  `MyService`  class has a dependency on  `MyDependency`, which is passed as an argument to the constructor. The  `final`  keyword is used to ensure that the  `myDependency`  field is set only once and cannot be changed.

### Setter Injection

Setter injection, on the other hand, involves calling  setter methods  on the object to set the dependencies. Here's an example:

```
public class MyService {
    private MyDependency myDependency;
    
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
    
    // ...
}

```

In this example, the  `MyService`  class has a  setter method  `setMyDependency`  that sets the  `myDependency`  field.

### Choosing between Constructor and Setter Injection

Both constructor and setter injection have their pros and cons. Constructor injection ensures that the dependencies are set at the time of  object creation  and cannot be changed later. Setter injection, on the other hand, allows for more flexibility and can be used to set  optional dependencies.

In general, it's recommended to use constructor injection for  mandatory dependencies  and setter injection for optional dependencies.

## Step 8 - Spring Framework Modules

Spring Framework is a  modular framework, which means that it is composed of several modules, each of which provides a different set of features and functionality. Here are some of the core modules of Spring:

### Spring Core

The  Spring Core module  provides the basic components of the Spring Framework, including the  IoC container  and DI functionality. This module is the foundation of the Spring Framework and is required by all other modules.

### Spring MVC

The  Spring MVC module  provides a web framework for building  web applications  using Spring. It includes features such as  request mapping,  data binding, and  view resolution.

### Spring Data

The Spring Data module provides a  unified API  for accessing various types of  data sources, including relational databases, NoSQL databases, and more. It includes modules such as  Spring Data JPA,  Spring Data MongoDB, and  Spring Data Redis.

### Spring Security

The  Spring Security module  provides security features for Spring applications, including authentication and authorization. It includes features such as  user authentication, access control, and  secure communication.

### Spring Boot

Spring Boot is a framework for building standalone Spring applications that are easy to deploy and run. It includes features such as auto-configuration, embedded servers, and production-ready metrics.

### Spring Cloud

Spring Cloud  is a collection of tools and frameworks for building distributed systems and microservices using Spring. It includes modules such as  Spring Cloud Config,  Spring Cloud Netflix, and  Spring Cloud Stream.

### Spring Integration

Spring Integration  is a framework for building message-driven applications using Spring. It includes features such as  channel adapters,  message routers, and  message transformers.

## Conclusion

Spring Framework is a powerful and popular framework for building Java applications. In this tutorial, we learned about constructor and setter injection in Spring, as well as the  core modules  of the Spring Framework. By understanding these concepts, you'll be well on your way to building robust and maintainable Spring applications.

## Step 10 - Why is Spring Framework Popular in the Java World?

Spring Framework is one of the most popular frameworks for building Java applications. Here are some of the reasons why:

### Dependency Injection

Spring Framework provides a powerful and flexible  dependency injection mechanism  that makes it easy to manage dependencies and decouple components in a Java application. With Spring's IoC container, you can easily wire together your application's components and manage their lifecycle.

### Modularity

Spring Framework is designed to be modular, which means that you can use only the components and features that you need in your application. This makes it easy to build applications that are lightweight and optimized for performance.

### Integration

Spring Framework provides integration with a wide variety of other technologies and frameworks, including  Hibernate,  JPA, and many others. This makes it easy to build applications that work seamlessly with existing systems and technologies.

### Testability

Spring Framework's modularity and  dependency injection  mechanism make it easy to write  unit tests  for your Java applications. With Spring, you can easily mock dependencies and test each component of your application in isolation.

### Community

Spring Framework has a large and active community of developers and users who contribute to the project and provide support to others. This makes it easy to find help and resources when you need them, and ensures that the framework is constantly evolving and improving.

## Step 17 - DO NOT SKIP: New to Maven and Eclipse

If you're new to Maven and Eclipse, here's a quick overview of how to get started:

1.  Install Eclipse: Download and install Eclipse from the official website.
    
2.  Install Maven: Download and install Maven from the official website.
    
3.  Create a new  Maven project: In Eclipse, go to File > New > Maven Project. Follow the prompts to create a new Maven project.
    
4.  Add dependencies: To add dependencies to your project, add them to the "pom.xml" file in your project. Maven will automatically download and manage the dependencies for you.
    
5.  Build and run your project: To build and run your project, use the  Maven commands  "mvn clean install" and "mvn exec:java" respectively.
    

Here's an example of a simple Maven project:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

```

In this example, we've defined a Maven project with a single dependency on  JUnit  4.12. When we buildand run the project using Maven, it will automatically download and include the  JUnit library  in our project.

To summarize, Maven is a powerful  build tool  that makes it easy to manage dependencies and build Java projects. Eclipse is a popular  IDE  that provides an  integrated environment  for developing Java applications. By using Maven and Eclipse together, you can streamline your development process and build high-quality, maintainable Java applications.

## 19. Step 11 - Dependency Injection - A few more examples

Dependency injection is a core concept in the Spring framework and allows for a more modular and flexible design of applications. In this step, we will go through a few more examples of how to use dependency injection in Spring.

### Constructor Injection

Constructor injection is a type of dependency injection where dependencies are injected through a constructor. For example, let's say we have a class  `Foo`  that depends on an interface  `Bar`. We can inject the dependency through the constructor as follows:

```
public class Foo {
    private Bar bar;

    public Foo(Bar bar) {
        this.bar = bar;
    }
}

```

### Setter Injection

Setter injection is a type of dependency injection where dependencies are injected through setter methods. For example, let's say we have a class  `Foo`  that depends on an interface  `Bar`. We can inject the dependency through a  setter method  as follows:

```
public class Foo {
    private Bar bar;

    public void setBar(Bar bar) {
        this.bar = bar;
    }
}

```

## 20. Step 12 - Autowiring in Depth - by Name and @Primary

Autowiring is a feature in Spring that allows the framework to automatically inject dependencies into a bean without the need for explicit configuration. In this step, we will go through autowiring in more depth and cover how to use it by name and with the  `@Primary`  annotation.

### Autowiring by Name

Autowiring by name is a way of  autowiring dependencies  in Spring by matching the  bean name  with the name of the dependency. For example, let's say we have a class  `Foo`  that depends on a bean with the name  `bar`. We can autowire the dependency by name as follows:

```
public class Foo {
    @Autowired
    private Bar bar;
}

```

### @Primary Annotation

The  `@Primary`  annotation is used to indicate that a bean should be considered the  primary bean  when multiple beans of the same type are present. For example, let's say we have two beans of type  `Bar`:

```
@Component
public class BarOne implements Bar {}

@Component
@Primary
public class BarTwo implements Bar {}

```

In this case, if we autowire a  `Bar`  dependency, Spring will inject an instance of  `BarTwo`  because it is marked as the primary bean.

## 21. Step 13 - Autowiring in Depth - @Qualifier annotation

The  `@Qualifier`  annotation is used in Spring to specify which bean to autowire when there are multiple beans of the same type. For example, let's say we have two beans of type  `Bar`:

```
@Component
@Qualifier("one")
public class BarOne implements Bar {}

@Component
@Qualifier("two")
public class BarTwo implements Bar {}

```

In this case, if we want to autowire a  `Bar`  dependency with the  `one`  qualifier, we can use the  `@Qualifier`  annotation as follows:

```
public class Foo {
    @Autowired
    @Qualifier("one")
    private Bar bar;
}

```

This tells Spring to inject an instance of  `BarOne`  because it is the bean with the  `one`  qualifier.
## 22. Step 14 - Scope of a Bean - Prototype and Singleton

In Spring, the scope of a bean defines the lifecycle and visibility of the bean instance. The two most common scopes in Spring are prototype and singleton.

### Singleton Scope

The default scope in Spring is singleton, which means that only one instance of the bean is created and shared for all requests for that bean. For example, let's say we have a class  `Foo`:

```
@Component
public class Foo {}

```

By default, Spring will create a single instance of  `Foo`  and share it across all requests for  `Foo`.

### Prototype Scope

Prototype scope in Spring means that a new instance of the bean is created for each request for that bean. For example, let's say we have a class  `Bar`:

```
@Component
@Scope("prototype")
public class Bar {}

```

In this case, each time we request a  `Bar`  instance from Spring, a new instance of  `Bar`  will be created.

## 23. Step 15 - Complex Scope Scenarios of a Spring Bean - Mix Prototype and Singleton

In more complex scenarios, we may want to mix prototype and  singleton scopes  for different beans. For example, let's say we have a class  `Foo`  that depends on a prototype-scoped bean  `Bar`:

```
@Component
public class Foo {
    @Autowired
    private Bar bar;
}

@Component
@Scope("prototype")
public class Bar {}

```

In this case, each time we request a  `Foo`  instance from Spring, a new instance of  `Bar`  will be created and injected into  `Foo`.

## 24. Step 15B - Difference Between Spring Singleton and GOF Singleton

It is important to note that the  Spring singleton scope  is different from the  singleton pattern  in the  Gang of Four  (GOF) design patterns. In the GOF singleton pattern, there is only one instance of a class globally, whereas in  Spring singleton  scope, there is only one instance of a bean per Spring container.

For example, let's say we have a class  `SingletonClass`  implemented as a GOF singleton:

```
public class SingletonClass {
    private static SingletonClass instance = new SingletonClass();
    private SingletonClass() {}
    public static SingletonClass getInstance() {
        return instance;
    }
}

```

In this case, there is only one instance of  `SingletonClass`  globally.

On the other hand, if we have a  Spring bean  with  singleton scope:

```
@Component
public class SingletonBean {}

```

In this case, there is only one instance of  `SingletonBean`  per Spring container.
Let's consider an example to illustrate this difference. Suppose we have a simple bean called  `Counter`  that increments an  internal counter  each time it is called:

```
@Component
@Scope("prototype")
public class Counter {
    private int count = 0;

    public int increment() {
        return ++count;
    }
}

```

If we inject this bean into another bean as a prototype, a new instance of  `Counter`  will be created each time it is requested:

```
@Component
public class PrototypeBean {
    @Autowired
    private Counter counter;

    public int incrementCounter() {
        return counter.increment();
    }
}

```

On the other hand, if we inject this bean into another bean as a singleton, only one instance of  `Counter`  will be created and shared among all requests:

```
@Component
@Scope("singleton")
public class SingletonBean {
    @Autowired
    private Counter counter;

    public int incrementCounter() {
        return counter.increment();
    }
}

```

Now, let's test these two scenarios by creating a new instance of each bean and invoking the  `incrementCounter()`  method on each:

```
@Component
public class Test {
    @Autowired
    private PrototypeBean prototypeBean;

    @Autowired
    private SingletonBean singletonBean;

    public void runTest() {
        // Prototype scope
        System.out.println("Prototype scope:");
        System.out.println(prototypeBean.incrementCounter()); // 1
        System.out.println(prototypeBean.incrementCounter()); // 1

        // Singleton scope
        System.out.println("Singleton scope:");
        System.out.println(singletonBean.incrementCounter()); // 1
        System.out.println(singletonBean.incrementCounter()); // 2
    }
}

```

In the prototype scope, a new instance of  `Counter`  is created each time  `incrementCounter()`  is called, so the counter is always reset to zero. In the  singleton scope, only one instance of  `Counter`  is created, so the counter is incremented each time  `incrementCounter()`  is called. Therefore, the output of this test would be:

```
Prototype scope:
1
1
Singleton scope:
1
2

```

As we can see, the behavior of the two scenarios is different due to the difference in scope. The  prototype scope  creates a new instance of the bean each time it is requested, while the singleton scope creates only one instance of the bean that is shared among all requests.

# Step 16 - Using Component Scan to scan for beans

In Spring  Framework, we can use component scan to scan for beans in our application. Component scan is a way to automatically detect and register beans in the  Spring container  based on certain criteria such as  class annotations.

## Enabling Component Scan

We can enable component scan in our  Spring application  by adding the  `@ComponentScan`  annotation to a configuration class. For example:

```
@Configuration
@ComponentScan("com.example.demo")
public class AppConfig {
    // configuration code here
}

```

In the above example, we have enabled component scan for the package  `com.example.demo`. This means that  Spring  will scan this package and its sub-packages for classes with certain annotations (such as  `@Component`,  `@Service`,  `@Repository`, etc.) and register them as beans in the Spring container.

## Defining Component Scan Filters

We can also define filters for component scan to include or exclude certain classes from being registered as beans. There are several types of filters we can use, such as  `@ComponentScan.Filter`,  `RegexPatternTypeFilter`,  `AspectJTypeFilter`, etc.

For example, if we want to include only classes annotated with  `@Controller`  in our component scan, we can do:

java

Copy

```
@Configuration
@ComponentScan(basePackages = "com.example.demo", includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, value = Controller.class))
public class AppConfig {
    // configuration code here
}

```

In the above example, we have used  `@ComponentScan.Filter`  to define an  annotation filter  that includes only classes annotated with  `@Controller`.

# Step 17 - Lifecycle of a Bean - @PostConstruct and @PreDestroy

In Spring Framework, the lifecycle of a bean refers to the various stages in the life of a bean, from its creation to its destruction. During the lifecycle of a bean, we can perform certain actions, such as initializing the bean, cleaning up resources, etc. We can use the  `@PostConstruct`  and  `@PreDestroy`  annotations to define methods that should be executed after the bean has been created and before the bean is destroyed, respectively.

## @PostConstruct Annotation

The  `@PostConstruct`  annotation is used to specify a method that should be called immediately after the bean has been created, and after all dependencies have been injected. The method annotated with  `@PostConstruct`  can be used to perform any  initialization logic  for the bean.

For example:

```
@Component
public class MyBean {
 
    @PostConstruct
    public void init() {
        // initialization logic here
    }
}

```

In the above example, the  `init()`  method will be called immediately after the  `MyBean`  has been created, and after all dependencies have been injected.

## @PreDestroy Annotation

The  `@PreDestroy`  annotation is used to specify a method that should be called just before the bean is destroyed. The method annotated with  `@PreDestroy`  can be used to perform any  cleanup logic  for the bean.

For example:

```
@Component
public class MyBean {
 
    @PreDestroy
    public void cleanup() {
        // cleanup logic here
    }
}

```

In the above example, the  `cleanup()`  method will be called just before the  `MyBean`  is destroyed. This method can be used to release any resources held by the bean, such as closing a database connection or releasing a file handle.

It is important to note that the  `@PostConstruct`  and  `@PreDestroy`  annotations only work with singleton scoped beans. If a bean is defined with a different scope, such as  prototype scope, these annotations will not be effective.
## Step 19 - Removing Spring Boot in Basic Application

In this step, we remove the  Spring Boot  framework from our basic application and replace it with the Spring Framework. Here are the steps we need to follow:

1.  Remove the  `spring-boot-starter-web`  dependency from the  `pom.xml`  file.
2.  Add the  `spring-webmvc`  and  `spring-context`  dependencies to the  `pom.xml`  file.
3.  Create a  `WebAppInitializer`  class that extends the  `AbstractAnnotationConfigDispatcherServletInitializer`  class.
4.  In the  `WebAppInitializer`  class, implement the  `getRootConfigClasses()`  and  `getServletConfigClasses()`  methods to define the  root configuration  and the  servlet configuration.
5.  Create a  `WebConfig`  class that extends the  `WebMvcConfigurerAdapter`  class and annotate it with the  `@Configuration`  annotation.
6.  In the  `WebConfig`  class, override the  `configureDefaultServletHandling()`  method and call the  `enable()`  method on the  `DefaultServletHandlerConfigurer`  object.
7.  In the  `WebConfig`  class, create a  `ViewResolver`  bean to configure the view resolver.
8.  Create a controller class that handles requests and returns a view.

## Step 20 - Fixing minor stuff - Add Logback and Close Application Context

In this final step, we add the  Logback logging framework  to our application and make sure that the application context is closed properly when the application shuts down.

1.  Add the  Logback dependencies  to the  `pom.xml`  file:

```
<dependencies>
    <!-- ... -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-core</artifactId>
        <version>1.2.3</version>
    </dependency>
</dependencies>

```

2.  Create a  `logback.xml`  file in the  `src/main/resources`  directory to configure Logback. Here's an example configuration:

```
<configuration>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    <root level="DEBUG">
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>

```

Note: The above  Logback configuration  will log messages to the console in a specific format.

3.  In the  `WebConfig`  class, add the following method to configure Logback:


```
@Bean
public LoggerContext loggerContext() {
    return (LoggerContext) LoggerFactory.getILoggerFactory();
}

```

4.  In the  `Main`  class, add the following code to close the application context when the application shuts down:


```
public static void main(String[] args) {
    try (AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class)) {
        // Run the application
    } catch (Exception e) {
        LOGGER.error("Error while running the application", e);
    }
}

```

Note: The  `AnnotationConfigApplicationContext`  class implements the  `AutoCloseable`  interface, which means that we can use it in a try-with-resources statement to automatically close the  application context  when the application exits.

## Step 21 - Defining Spring Application Context using XML - Part 1

In this step, we will be defining the  Spring application context  using XML.

### What is  Spring Application  Context?

The Spring  application context is a container that holds all the beans (objects) required by the application. It creates, manages, and wires the beans together. The  Spring framework  provides various implementations of the application context, such as XML-based, annotation-based, and Java-based.

### How to Define Spring Application Context using XML?

To define the Spring application context using XML, we need to create a  configuration file  named  `applicationContext.xml`  in the  `src/main/resources`  directory. This file will contain the bean definitions.

Here's an example of  `applicationContext.xml`  file:

```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="greetingService" class="com.example.service.GreetingServiceImpl">
        <property name="greeting" value="Hello, World!"/>
    </bean>

    <bean id="greetingController" class="com.example.controller.GreetingController">
        <property name="greetingService" ref="greetingService"/>
    </bean>

</beans>

```

In this example, we have defined two beans -  `greetingService`  and  `greetingController`. The  `greetingService`  bean is of type  `GreetingServiceImpl`, which is a service that provides a greeting message. The  `greetingController`  bean is of type  `GreetingController`, which is a controller that uses the  `greetingService`  to get the  greeting message  and returns it to the client.

### How to Use Spring Application Context in Code?

To use the Spring application context in code, we need to create an instance of  `ClassPathXmlApplicationContext`  by passing the  configuration file path  as a parameter. Here's an example:

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
GreetingController greetingController = context.getBean(GreetingController.class);
String result = greetingController.greet();
System.out.println(result);

```

In this example, we have created an instance of  `ClassPathXmlApplicationContext`  by passing the  `applicationContext.xml`  file path as a parameter. We have then retrieved the  `GreetingController`  bean from the context and called its  `greet()`  method, which returns the greeting message. The message is then printed to the console.

## Step 22 - Defining Spring Application Context using XML - Part 2

In the previous step, we learned how to define the Spring application context using XML. In this step, we will cover some advanced features of  Spring XML configuration.

### Property Placeholder

Spring provides a way to externalize the configuration using property files. We can define placeholders in the  XML configuration file  and use property files to replace those placeholders at runtime.

Here's an example of how to define a  property placeholder  in the XML configuration file:

```
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

```

In this example, we have defined a bean of type  `BasicDataSource`  and used property placeholders for the  driver class name,  URL, username, and password. We can replace these placeholders with actual values at runtime by defining them in a property file.

Here's an example of a  property file  named  `application.properties`:


```
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mydb
jdbc.username=root
jdbc.password=password

```

We can load this property file at runtime using  `PropertyPlaceholderConfigurer`.

```
<context:property-placeholder location="classpath:application.properties"/>

```

### Bean Scopes

Spring provides several scopes for beans, such as singleton, prototype, request, session, and global session. The default scope is singleton, which means Spring creates only one instance of the bean and returns the same instance every time it is requested.

Here's an example of how to define a  prototype scope  for a bean:

xml

Copy

```
<bean id="myBean" class="com.example.MyBean" scope="prototype"/>

```

In this example, we have defined a bean of type  `MyBean`  with a prototype scope. This means Spring creates a new instance of the bean every time it is requested.

### Bean Inheritance

Spring provides a way to inherit  bean definitions. We can define a  parent bean  and then create  child beans  that inherit the properties of the parent bean.

Here's an example of a parentbean:

```
<bean id="parentBean" class="com.example.Parent">
    <property name="name" value="Parent"/>
</bean>

```

And here's an example of a  child bean  that inherits from the parent bean:

```
<bean id="childBean" class="com.example.Child" parent="parentBean">
    <property name="age" value="10"/>
</bean>

```

In this example, we have defined a parent bean of type  `Parent`  with a name property. We have then defined a child bean of type  `Child`  that inherits from the parent bean and adds an age property.

### Aliases

Spring provides a way to define  aliases  for beans. We can define multiple aliases for a single bean.

Here's an example of how to define aliases for a bean:

```
<bean id="myBean" class="com.example.MyBean"/>
<alias name="myBean" alias="myAlias"/>
<alias name="myBean" alias="myOtherAlias"/>

```

In this example, we have defined a bean of type  `MyBean`  with an id of  `myBean`. We have then defined two aliases for the bean -  `myAlias`  and  `myOtherAlias`.

## Step 23 - Mixing XML Context with Component Scan for Beans defined with Annotations

In the previous steps, we have learned how to define the Spring application context using XML. We have also learned how to use  component scanning  to automatically detect and register beans defined with annotations. In this step, we will learn how to mix XML context with component scan.

### Why Mix XML Context with Component Scan?

Although component scanning is a powerful feature of Spring, there may be cases where we need to define beans using XML configuration. For example, we may need to define beans with  complex initialization logic  or we may need to use property placeholders. In such cases, we can mix  XML context  with component scan.

### How to Mix XML Context with Component Scan?

To mix XML context with component scan, we can define the XML configuration file and enable component scanning in the same application context.

Here's an example of how to define the XML configuration file:

```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <context:property-placeholder location="classpath:application.properties"/>

    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <bean id="myBean" class="com.example.MyBean"/>

</beans>

```

In this example, we have defined two beans using  XML configuration  -  `dataSource`  and  `myBean`. We have also loaded property placeholders from the  `application.properties`  file.

To enable component scanning, we can add the following line to the XML configuration file:

```
<context:component-scan base-package="com.example"/>

```

This tells Spring to scan the  `com.example`  package for beans defined with annotations.

We can then use the beans defined in the XML configuration file and the beans detected by component scanning in the same application context.

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
MyBean myBean = context.getBean(MyBean.class);
myBean.doSomething();

```

In this example, we have created an instance of  `ClassPathXmlApplicationContext`  by passing the  `applicationContext.xml`  file path  as a parameter. We have then retrieved the  `MyBean`  bean from the context and called its  `doSomething()`  method. The  `MyBean`  bean is defined using XML configuration.

A property placeholder is a placeholder used in the  Spring XML configuration file  to specify a value that can be resolved at runtime from a property file or environment variables. It allows us to externalize the configuration and change values at runtime without modifying the code.

Here's an example of how to define a  property placeholder  in the Spring XML configuration file:


```
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

```

In this example, we have defined a bean of type  `BasicDataSource`  and used property placeholders for the  driver class name,  URL, username, and password.

We can replace these placeholders with actual values at runtime by defining them in a  property file. Here's an example of a property file named  `application.properties`:

```
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mydb
jdbc.username=root
jdbc.password=password

```

We can then load this property file at runtime using  `PropertyPlaceholderConfigurer`:

```
<context:property-placeholder location="classpath:application.properties"/>

```

This will replace the placeholders in the Spring  XML configuration file  with the values from the  `application.properties`  file at runtime.

In Spring, an alias is an alternative name or identifier for a bean. It allows us to refer to a bean by multiple names. We can define one or more aliases for a single bean.

Here's an example of how to define aliases for a bean in the  Spring XML configuration file:

```
<bean id="myBean" class="com.example.MyBean"/>
<alias name="myBean" alias="myAlias"/>
<alias name="myBean" alias="myOtherAlias"/>

```

In this example, we have defined a bean of type  `MyBean`  with an id of  `myBean`. We have then defined two aliases for the bean -  `myAlias`  and  `myOtherAlias`.

We can then use any of these names to retrieve the bean from the  Spring application context:

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
MyBean myBean = context.getBean("myBean", MyBean.class);
MyBean myAlias = context.getBean("myAlias", MyBean.class);
MyBean myOtherAlias = context.getBean("myOtherAlias", MyBean.class);

```

In this example, we have retrieved the bean using the original name  `myBean`, as well as the aliases  `myAlias`  and  `myOtherAlias`. All three calls will return the same instance of the  `MyBean`  bean.
## IOC Container  vs Application Context vs  Bean Factory

In Spring, an Inversion of Control (IOC) container is responsible for managing the lifecycle of beans. It creates and manages instances of beans, and injects dependencies into them. There are two types of  IOC containers  in Spring:  BeanFactory  and ApplicationContext.

BeanFactory is the basic IOC container that provides the fundamental features of the IOC container. It reads  bean definitions  and creates  bean instances  lazily, i.e., only when they are requested. It is suitable for small to medium-sized applications where the performance is not a significant concern.

ApplicationContext is a sub-interface of BeanFactory that provides additional features like  AOP,  message resource handling,  event publication, and internationalization support. It reads bean definitions and creates bean instances eagerly, i.e., at the time of application startup. It is suitable for large, enterprise-level applications where the performance is a significant concern.

Here's an example that demonstrates the use of  ApplicationContext:

```
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        MyBean myBean = context.getBean("myBean", MyBean.class);
        myBean.doSomething();
    }
}

```

In this example, we have created an instance of the ApplicationContext by providing the path to the  XML configuration  file. We have then retrieved an instance of the  MyBean class  from the context and called its  `doSomething()`  method.

## @Component vs @Service vs @Repository vs @Controller

In Spring, we use annotations to mark classes as beans and to specify their roles. There are four annotations that are commonly used to mark classes as beans:  `@Component`,  `@Service`,  `@Repository`, and  `@Controller`.

`@Component`  is the most basic annotation that marks a class as a Spring bean. It is used to indicate that a class is a general-purpose component that does not fall into any specific category.

`@Service`  is an annotation that marks a class as a business service. It is used to indicate that a class performs some  business logic  and is usually used in the service layer of the application.

`@Repository`  is an annotation that marks a class as a data access object (DAO). It is used to indicate that a class performs database operations and is usually used in the  persistence layer  of the application.

`@Controller`  is an annotation that marks a class as a controller. It is used to indicate that a class handles  HTTP requests  and is usually used in the  presentation layer  of the application.

Here's an example that demonstrates the use of  `@Service`:

```
@Service
public class MyService {
    public void doSomething() {
        // business logic here
    }
}

```

In this example, we have marked the  MyService  class with  `@Service`  to indicate that it is a business service. We can then inject an instance of this class into other beans using  `@Autowired`.

## Read values from external properties file

In Spring, we can  externalize configuration  by storing values in an  external properties file. We can then read these values into our  Spring beans  using  `@Value`  annotations.

Here's an example of how to define properties in an external properties file:

```
my.property=value

```

We can then read this property into a  Spring bean  using  `@Value`:

```
@Service
public class MyService {
    @Value("${my.property}")
    private String myProperty;

    public void doSomething() {
        System.out.println("my.property = " + myProperty);
    }
}

```

In this example, we have injected the value of the  `my.property`  key into the  `myProperty`  field of the  MyService bean  using  `@Value`. We can then use this value in our business logic. We can also use  `@PropertySource`  to specify the location of the properties file.

```
@Service
@PropertySource("classpath:my.properties")
public class MyService {
    @Value("${my.property}")
    private String myProperty;

    public void doSomething() {
        System.out.println("my.property = " + myProperty);
    }
}

```

In this example, we have used  `@PropertySource`  to specify the location of the  properties file. We can then inject the value of the  `my.property`  key into the  `myProperty`  field of the MyService bean using  `@Value`.

## Understanding the World Before Spring Boot

Before Spring Boot, building a Spring-based application required a lot of manual configuration. It involved setting up a project with the required dependencies, configuring the web server, setting up the  database connection, and configuring the  Spring framework  itself.

Developers had to spend a significant amount of time and effort in configuring the application, which often led to configuration errors and inconsistencies.  Spring Boot  aims to simplify this process by providing a set of  opinionated defaults  and auto-configuration features.

## Setting up  New Spring  Boot Project with Spring Initializr

Spring Initializr is a web-based tool that allows developers to quickly generate a new  Spring Boot project  with the required dependencies and configurations. It provides a simple user interface to configure the project, select the required dependencies, and download the project as a zip file.

Here's an example of how to create a new Spring Boot project using  Spring Initializr:

1.  Go to  [https://start.spring.io/](https://start.spring.io/)
2.  Select the required  project metadata  such as Group, Artifact and dependencies
3.  Click "Generate" button and download the  project zip file
4.  Extract the  zip file  to a new directory in your local machine

## Build a Hello World API with Spring Boot

Now that we have set up a new Spring Boot project, let's build a simple  Hello World API  using Spring Boot.

Here's an example of how to build a simple Hello World API with Spring Boot:

1.  Create a new Spring Boot project using Spring Initializr
2.  Open  `src/main/java/com/example/demo/DemoApplication.java`
3.  Add a  `@RestController`  annotation to the class to indicate that it is a REST controller
4.  Add a  `@GetMapping`  annotation to a method in the class to handle  GET requests
5.  Return a simple string from the method
6.  Run the application using  `./mvnw spring-boot:run`  command
7.  Open a  web browser  and navigate to  `http://localhost:8080`

```
@RestController
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/")
    public String hello() {
        return "Hello, World!";
    }
}

```

In this example, we have annotated the  `DemoApplication`  class with  `@RestController`  and  `@SpringBootApplication`. We have also added a  `@GetMapping`  annotation to the  `hello()`  method to handle GET requests.

When we run the application using  `./mvnw spring-boot:run`  command, Spring Boot starts an  embedded Tomcat server  and deploys our application to it. We can then open a web browser and navigate to  `http://localhost:8080`  to see the "Hello, World!" message returned by the API.
