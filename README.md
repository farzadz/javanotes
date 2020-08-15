# Java Notes


### Copy Constructor vs. Inhertied copy method

Direct use of copy constructor when working with collections of parent objects leads to collection of concrete parent objects as the copy constructor of the parent object gets called, not the copy constructor of the child. 

[see](https://www.baeldung.com/java-copy-constructor)
```java

public class Init {

  public static void main(String[] args) {
    Parent p = new Child("Jack", 12);
    Parent cloned = new Parent(p);
    if (cloned instanceof Child) {
      // not executed
      System.out.println("Created child via direct use of copy constructor");
    }

    cloned = p.copy();
    if (cloned instanceof Child) {
      // executes
      System.out.println("Created child via copy method");
    }

  }

  static class Parent {

    private String name;

    public Parent(String name) {
      this.name = name;
    }

    public Parent(Parent parent) {
      this.name = parent.getName();
    }

    public Parent copy() {
      return new Parent(this);
    }

    public String getName() {
      return name;
    }

  }

  static class Child extends Parent {

    private int age;

    public Child(String name, int age) {

      super(name);
      this.age = age;
    }

    public Child(Child child) {
      super(child.getName());
      this.age = child.age;
    }
    
    @Override
    public Parent copy() {
      return new Child(this);
    }
  }
}
```
