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
