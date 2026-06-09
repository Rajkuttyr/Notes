Two classes 
Pattern and matcher
patern  to create a pattern we must invoke it static compile method which will return a pattern object 
accept regex as arg
Matcher - interupts the patern and perfoms match operation against an input String to obtain a matcher object we must invokemethod on a Pattern object

```java
Pattern pat = Pattern.compile("[A-Z].[fk]e");
Matcher matcher - pattern.matcher("Like");
boolean matches = matcher.matches();
System.out.printl(matches);
```
FInd the next expression that matches the pattern within the same input string by starting at the very first index of that string
```java
Pattern pattern = Pattern.compile("[A-Z][a-z]");
Matcher matcher = pattern.matcher("Rajkutty");
for(int i=0;i<5;i++){
boolean match = matche.find();
System.out.println(match);
}

