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

