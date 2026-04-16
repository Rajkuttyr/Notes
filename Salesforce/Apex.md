Apex is a object oriented programing language which is propitery language developed by salesforce.com to allow us to write code that executes on the 
force.com platform
it is used for building SAAS applicstion on top of Salesforce.com
Apex is Saved,compiled and execute on the server 
80 to 90 similar to java
salesforce - admin course
salesforce suite of CRM product it is a platform to build SAAS application 
Apex is used to develop the logic it is used to accompans 
Apex works on MVC which is Modelur view controller
controller can be built using pointing click tool or using apex
when to use Apex
1. T perform complex buisness process which are not supported by workflow process
2. to perform complex validation over multiple objects
3. To create web service and email sevice 
4. for transactions and roll back 
Features not supported
it cannot show the ui elements other than error message

Apex is used only on the controller part
It cannot change the standard sdfc functionality but can be used to stop its execution or to add new functionality -can be overriden 
it canot be used to create a temp fil
it cannpt crearte multithread
Apex environment
1. production environment
2. development 
we can run apex in developer production and sandbox
production org we cannot use apex
al developent in sandbox envirnment in produv=ction
tools to write apex code
force.com console 
code editor in sales force inteface


Apex Variables
Variable named value holder 
similar to java and rules are also similar 
name of variable is called Identifier
Integer num;
Apex Constants 
Apex constant are the variable whose value cannot be changed after declares;
it can be done by declaring the keyword with final key word
eg final integer a =5;
anything declared as final method cannot be overide
if you dont want a method to be overiden it can be marked as final
by default methods are final aslo classes are by default final

Flows of Action 
![[Pasted image 20260406230930.png]]

while saving it automatically get compiled and svaed

Data Types in Apex
Apex is strongly typed 
Every variable i stype
variable is used to store or refernce an value of a declared datatype on the memory
primitive user defined
primitive datatype
Integer data type used to store a integer numeric value
Integer is divided into two type int and long

```java

public class newClass {
    public static void myMethod(){
        integer a;
        a=50;
        integer a1 =50;
        long l1;
        l1=89989;
        long l2 =678909789L;
        long l3 = 214737l;
        decimal = 784;
        String s ='Raj';
        String s1 ='A';
        String s2=s+s1;//concatination
        Date d1;
        d1=Date.today();//current date
        d1=Date.newInstances(2018,01,01);//2018-01-01
        //methods
        d1=d1.toStartOfMonth();
        d1=d1.toStartOfWeek();
        d1=d1.addDays(5);
        d1=d1.addYears(5);
        d1=d1.Months(5);
        //Time
        Time t1=Time.newInstances(hr,min,sec,ms);
        t1.addHours(2);
        t1.addMinutes(20);
        
        DateTime dt1=DateTime.newInstances(2018,05,15,09,20,30);
        boolean b =true;
        boolean b1 = fale;
        boolean b2 =5>7;
        
        
        
    }

}
```
Floating used to store a decimal value;
no datatype is called as char in Apex
stting should be enclosed in single qotes
Date data type is used to represent date

Rules of Conversion
to convert a value into another 
lower to higher it automatically converts
to convert higher t lower for explict mention
Hieracy of numbers int<long<double<decimal.
ID can be always assigned to strings
Strings can be assigned to id

Enum 
Enum 
```java
public enum Season{
Winter,Summer,Spring,Fall
}
```
Sobject are basically used to represent a single record in the database 
Apex is aldready integrated with database
single object return the 
sobject if yoou want to represent s object 
```java
public class sObjectClass{
Accout a1 = new Account();
Contact c1 = new Contact();
Account a2 = new Account(Name='Amazon');
a1.Name = 'Raj';
Student__c st1 = new Student__c(Student_name__c ='Avinash');


}
```
Sobject values to the Sobject can be assigned through constructor or through Dot notation
to add custom object "underscore underscore__c" at the end of the identifier

Collection 
we will use collection in order to store simillar type of information together we use collection 
In apex we have three collection
List set and Map
List
In list the element or values or stored in order like first in first second in second
The elements in the List can have duplicate value
List is similar t arrya in java
first element 0 

```java
public class ListClass{
List<Datatype> lList = new List<DataType>();
List<Integer> llist = new List<Integer>();
ll.add(2);
ll.add(4);
ll.add(6);
List<Integer> l2  = new List<Integer>{2,4,6};
l2.add(5);
}
```
List Array Notation 
List array Notation ;
```java
Integer[] l4 = new Integer[4];
Integer[] l5 = new List<Integer>();
List<Integer> l6 = new Integer[4];
l6[0]=10;
System.debug(l6[0])//10;

```
Array is dynamic similar to List in Apex
Method in List 
```java
System.debug(l6.size());
System.debug(l6.get(2));// return the elemrnt at index 2
l6.remove(2);
List<Integer> l7 = new Integer<>();
l7 = l6.clone();
l7.set(0,50);//set element at index position;
l7.sort();
System.debug(l2.isEmpty());
l7.clear();

```
while removing the element from the list the next element will be shifted
Sets 
1. element in list are not ordererd where us in set is ordered
2. Elements in the set are unique;
```java
Set<Datatype> s = new Set<DataTye>();
s1.add(2);
Swr<Integer> s2 = new Set<Integer>{1,2,3};
s2.size();
```

Map
Map is key value pair 
key is unique and value is not unique
store the name and roll number similar to Hashmap in java
