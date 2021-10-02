# Java-Basic

* If there is no public class in a java program, we can use any name for that java file. We can choose any name to save the following file i.e. ```anything.java```, ```others.java```, ```sample.java``` etc.
```
clas A {....}
clas B {....}
clas C {....}
```

* A java program can contain at most one public class and that program must be saved with that public class name. To save the following file, we must save it as ```Sample.java```
```
public class Sample {...}
class One {...}
class Two {...}
```

* We compile java programs, not java classes. A java program can contain multiple classes. When we compile, we compile ```.java files```. After compilation, ```.class``` files are generated from that ```.java``` file and then we run the ```.class``` files. If we save the following file as ```Sample.java``` and compile using ```javac Sample.java``` , three ```.class``` files will be generated named ```One.class```,```Two.class```,```Three.class```. Now, we can run seperate ```.class``` files running command ```java One``` or ```java Two``` . To run a ```.class``` file, that class must contain a ```main()``` method. As ```Three.class``` doesn't contain ```main()``` method, it'll generate a runtime error. Though we saved the following file as Sample.java, we can't run this class using command ```java Sample``` as no ```.class``` file was generated for this one. <b> ```.class``` files are generated based on class declaration, not the file name.** </b>
```
class One { System.out.println("hello from one") ; }
class Two { System.out.println("hello from two") ; }
class Three {}
```

* Two packages are not required to be imported in any java program. 
  - java.lang package. [java.lang contains String,Thread,Exception,StringBuffer ......etc classes]
  - Current working directory/package i.e. class from same directory/package. If we put ```A.java``` and ```B.java``` under a same folder, We can use any one of them to another without importing them.

* If we import any package, only classes from those packages are imported, not the classes of sub packages. ```Pattern``` class is present inside java.util.regex package. If we want to use ```Pattern``` class, we'll have to implicitly import ```java.util.regex``` package. If we import ```java.*```, only classes present inside ```java``` pacakge will be imported. not the class from sub packages i.e. uitl,reges
```
   java
     |---------------------------------- by importing java.*, all classes form this level will be imported, not util classes.
     |---util
           |---------------------------- by importing java.util.*, all classes form java.util will be imported, not the regex classes.
           |--regex
                |----------------------- by importing java.util.regex, all class from java.util.regex will be imported. So, if we want to use Pattern class,we'll                   |                          have to import java.util.regex
                |---Pattern
```
* In any java program, at most one ```package``` statement is allowed. We can't use more than one package statements.
```
//Sample.java
package com.example.one ; 
package com.example.two ; //---------> compile time error
public class Sample { ..... }
```

* In any java program, first non-commented statement must be ```pacakge```. 
```
import java.util.* ; 
package com.example.one ; // ------> compile time error. package must be stated first. then import.
....
```

* 5 modifiers for top lever classes: ```public``` , ```<default>``` , ```abstract``` , ```final``` , ```strictfp```
* modifiers for inner classes: ```private```,```protected```,```static``` + above 5 modifiers   
* If no modifiers are declared i.e. <default> ,  in any class, It's accessable from any classes within <br>the same package</br>
* An abstract class can contain zero or more abstract methods. It means, we can declare any class as ```abstract``` even though it doesn't contain any abstract method. for example: ```HttpServlet``` class.



## ThreadGroup
A thread group contains a group of threads including subthreads based on functionality. Using thread groups, we can perform common operations very easily.

* main method belongs to main thread
* main thread belongs to main group.
* Every thread group is the child group of **System** group. 
```
private static void main(String[] args) {
	System.out.println(Thread.currentThread().getThreadGroup().getName()) ; // main
	System.out.println(Thread.currentThread().getThreadGroup().getParent().getName()) ; // system

}
```
* System group contains several system level threads. Some of them are:
  - Finalizer
  - Reference Handler
  - Signal Dispatcher
  - Attach Listener

## ThreadGroup constructors
```
private static void main(String[] args) {
	ThreadGroup tg1 = new ThreadGroup("first group");
	System.out.println(tg1.getParent().getName()); // main
	
	// customizing parent group
	ThreadGroup tg2 = new ThreadGroup(tg1, "second group");
	System.out.println(tg2.getParent().getName()); // first group
}
```
## Priorities of threads inside a group

   - Default priority of a thread group is 10.
   - Default priority of a thread is 5.
   - If we change the priority of a thread group, it won't affect the priority of existing threads inside the group. But, the newly added threads will assigned the updated priority of the gruop. 
   - In the following code, even if the default priority of a thread is 5, thread3 is supposed to get priority 5. But, as priority is set to 3 of the tg1 group, it'll get 3. But, thread1 and thread2 don't get affected. Their priority will be 5 as before. 
```
private static void main(String[] args) {
	ThreadGroup tg1 = new ThreadGroup("first group"); // priority 10
	Thread thread1 = new Thread(tg1, "first thread) ; // priority 5
	Thread thread2 = new Thread(tg1, "second thread) ; // priority 5

	tg1.setMaxPriority(3) ;
	Thread thread3 = new Thread(tg1, "third thread) ; // priority 3

	System.out.println(thread1.getPriority()); // 5
	System.out.println(thread2.getPriority()); // 5
	System.out.println(thread3.getPriority()); // 3
}
```
## Problems with traditional "Synchronized" keyword
   - No flexibility to try for a lock. Thread must wait to get the lock. Locks will be allocated to a thread based on thread scheduler.
   - There is no way to specify maximum waiting tiime for a thread to get the lock so that thread will wait until getting the lock which may create performance problem causing deadlock.
   - If a thread release a lock, we have no control which waiting thread will get the lock.
   - There is no api to list all waiting threads for a lock.
   - **Synchronized** keyword must be used either at method or within a method. It is not possible to use accross multiple methods. We can't achieve the following scenario using synchronized keyword. 
   ```
   void method1() {
	   //
	   // ------ at this point, we want to lock
	   method2();
	   //
	   //
   }
   void mehtod2() {
	   //-----
	   //-- at this point, we want to release the lock
	   //
   }
   ```


