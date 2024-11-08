---
title: Java Regular Expression
category: Blog
tags:
  - Java
---

## References
- https://www.rexegg.com/regex-lookarounds.php
- https://medium.com/stackera/java-regex-part-1-introduction-34d6a12ede8d

## Character classes:
```
. 	Represents for any characters
\d 	Represents for digits from 0 to 9; it is equivalent to [0-9]
\D 	Represents non-digits; or it is equivalent to [^0-9]
\s 	Represents for whitespace characters; including \t \n \f \r
\S 	Represents for non-whitespace characters; or it is equivalent to [^\s]
\w 	Represents for word characters including a-z A-Z 0-9 _; or it is equivalent to [a-zA-Z_0-9]
\W 	Represents for non-word characters; or it is equivalent to [^\w]
```

## Quantifiers
|  |  | 
| --------------- | --------------- |
| * | We have the star character means matching 0 or more times. For instance: <br>\d*: means the matched string can have 0 or more digits. <br>\w*: means the matched string can have 0 or more word characters from a to z, or digits from 0 to 9| 
| + | The plus sign means matching 1 or more times. For instance:<br>\d+: means the matched string can contain more than one digits<br>\w+: means the matched string can contain more than one word characters |
| ? | The question mark means matching 1 or 0 time. For instance:<br>\d?: means the matched string can contain 0 or 1 digit<br>\w?: means the matched string can contain 0 or 1 word | 
| {n} | n in braces means matching exactly n times. For instance:<br>\d{5}: means the matched string must contain exactly 5 digits<br>\w{3}: means the matched string must contain exactly 3 word characters | 
| {n,} | n comma in braces means matching at least n times. For instance:<br>\d{3,}: means the matched string must contain at least 3 digits<br>\w{4,}: means the matched string must contain at least 4 word characters | 
| {n,m} | And finally, we have n comma m means matching at least n times, but not more than m times. For instance:<br>\d{3, 5}: means the matched string must contain at least 3 digits, but not more than 5 digits<br>\w{1, 7}: means the matched string must contain at least 1 word, but not more than 7 word characters. |


## Boundary Matcher
| Meta character  | Meaning |
| ------------- | ------------- |
| ^  | matching at the beginning of the line, which we can use to check if the input string starts with a certain text.  |
| $  | matching at the end of the line, which we can use to check if the input string ends with a certain text.  |
| \b  | matching a word boundary, which we can use to check if the input string contains a whole word. This is the option we option see in searching features in many applications   |
| \B  | matching a non-word boundary, which we can use to find a certain word that start with some letters.  |


## String.matches()
```java
@Test
public void matches_digits() {
    assertTrue("4".matches("\\d"));
    assertFalse("41".matches("\\d"));
    assertFalse("-1".matches("\\d"));
    assertFalse("a".matches("\\d"));

    assertTrue("4123".matches("\\d+"));

    assertTrue("21".matches("\\d{2,4}"));
    assertTrue("123".matches("\\d{2,4}"));
    assertTrue("1234".matches("\\d{2,4}"));
    assertFalse("1".matches("\\d{2,4}"));
    assertFalse("12345".matches("\\d{2,4}"));

    assertTrue("ISBN-12345".matches("ISBN-\\d{5}"));
    assertFalse("ISBN12345".matches("ISBN-\\d{5}"));
    assertFalse("ISBN-1234".matches("ISBN-\\d{5}"));
}

@Test
public void matches_characters() {
    assertTrue("User123".matches("\\w+"));
    assertTrue("user123".matches("\\w+"));
    assertTrue("user123".matches("[a-z0-9A-Z]+"));

    assertFalse("user@123".matches("\\w+"));

    assertTrue("084-38-1234567".matches("\\d{3}-\\d{2}-\\d{7}"));

    assertTrue("88-1234567".matches("(\\d{3}-)?\\d{2}-\\d{7}"));
    assertTrue("123-88-1234567".matches("(\\d{3}-)?\\d{2}-\\d{7}"));
}
```
## String.replaceAll()
```java
@Test
public void replace_vs_replaceAll() {
    assertEquals(" This is a string with some typos ", " This is a strIng wIth some typos ".replace("I", "i"));
    assertEquals("This is a string that contains many typos", "This is 34a string 23that contain56s many typos".replaceAll("\\d+", ""));

    assertEquals("This is text with some special characters in in", "This is te$xt wi%th s*ome spe!cial characters in in".replaceAll("[^\\w ]", ""));
}
```

## String.split()
```java
@Test
public void split() {
    assertEquals(10, "I love you so much! But I cannot marry you.".split("[ ]+").length);
    String[] token = "I love you so much! But I cannot marry you.".split("[! .]+");
    assertEquals(10, token.length);
    assertEquals("you", token[9]);
    assertEquals("much", token[4]);
}
```

## Regex matches()
```java
@Test
public void pattern_matches() {
    var pattern = Pattern.compile("[a-zA-Z\\s]+");
    var matcher = pattern.matcher("David Karan");
    assertTrue(matcher.matches());

    matcher = pattern.matcher("David 123");
    assertFalse(matcher.matches());
}
```

## Regex lookingAt
```java
@Test
public void pattern_lookingAt() {
    var pattern = Pattern.compile("David");
    var matcher = pattern.matcher("David Karan");
    assertTrue(matcher.lookingAt());

    matcher = pattern.matcher("Allen David");
    assertFalse(matcher.lookingAt());
}
```

## Regex find()
```java
@Test
public void pattern_find() {
    String s = "I love you so much! However, I cannot marry you because you are NOT a human!";
    var pattern = Pattern.compile("not", Pattern.CASE_INSENSITIVE);
    var matcher = pattern.matcher(s);

    int count = 0;
    while(matcher.find()) {
        ++count;
    }
    assertEquals(2, count);

    s = "I love you 34 so much! However, 24 I cannot marry 45 you because 4 you are not a human!";
    pattern = Pattern.compile("\\d+");
    matcher = pattern.matcher(s);

    String[] token = {"34", "24", "45", "4"};
    for(String t : token) {
        matcher.find();
        assertEquals(t, matcher.group());
    }
}
```

## Regex group()
```java
@Test
public void pattern_group() {
    var pattern = Pattern.compile("(\\w+) (\\d{1,2})-(\\d{1,2})-(\\d{4})");
    var matcher = pattern.matcher("Monday 12-9-2013");

    matcher.find();
    assertEquals(4, matcher.groupCount());
    assertEquals("Monday", matcher.group(1));
    assertEquals("12", matcher.group(2));
    assertEquals("9", matcher.group(3));
    assertEquals("2013", matcher.group(4));
}
```

## Regex boundary
```java
@Test
public void pattern_boundary() {
    var pattern = Pattern.compile("^is$");
    assertTrue(pattern.matcher("is").find());
    assertFalse(pattern.matcher("is a").find());
    assertFalse(pattern.matcher("this").find());

    pattern = Pattern.compile("\\bis\\b");
    assertTrue(pattern.matcher("that is a bug").find());
    assertFalse(pattern.matcher("this and that").find());
    assertFalse(pattern.matcher("isn't it").find());

    pattern = Pattern.compile("\\Bis\\b");
    assertFalse(pattern.matcher("that is a bug").find());
    assertTrue(pattern.matcher("this and that").find());
}
```

## Regex back reference
```java
@Test
public void group_back_reference() {
    var pattern = Pattern.compile("(\\w\\w)\\1\\1");
    assertTrue(pattern.matcher("ababab").find());
    assertTrue(pattern.matcher("1ababab2").find());
    assertFalse(pattern.matcher("ababb").find());
}
```

## Regex reluctant
```java
/**
 * how the greedy and reluctant quantifiers work
 * First, the first group pattern consumed the whole text since it matched all the characters.
 * It then backtracked and slowly released each character that it had collected to give the
 * second group more opportunities to match
 */
@Test
public void no_greedy() {
    String s = "The order number is 8983";
    // greedy
    var pattern = Pattern.compile("(.*)(\\d+)");
    var matcher = pattern.matcher(s);
    matcher.find();
    assertEquals("The order number is 898", matcher.group(1));
    assertEquals("3", matcher.group(2));

    // reluctant
    pattern = Pattern.compile("(.*?)(\\d+)");
    matcher = pattern.matcher(s);
    matcher.find();
    assertEquals("The order number is ", matcher.group(1));
    assertEquals("8983", matcher.group(2));
}
```

## Regex possessive quantifiers
```java
/**
 * The possessive quantifiers work similarly to the greedy technique in the first step,
 * but differently in the second step in which it does not backtrack and release characters,
 * it had collected for the other groups to find a match. And this may significantly change
 * the matching results.
 */
@Test
public void possessive_quantifiers() {
    String text = "This is a very long string that does not end with digits ";
    for(int i = 0; i <10; ++i) text += text;

    // greedy version
    var pattern = Pattern.compile("(.*)\\d{4}");
    long start = System.currentTimeMillis();
    var matcher = pattern.matcher(text);
    matcher.find();
    long end = System.currentTimeMillis();
    System.out.println("Time elapsed: " + (end - start) + " ms");

    // possessive version
    pattern = Pattern.compile("(.*+)\\d{4}");
    start = System.currentTimeMillis();
    matcher = pattern.matcher(text);
    matcher.find();
    end = System.currentTimeMillis();
    System.out.println("Time elapsed: " + (end - start) + " ms");
}
```

## Regex look ahead
```java
@Test
public void look_ahead() {
    // Positive Look-Ahead
    // at least 1 digit and 1 uppercase letter, length from 4 to 8
    String password_pattern = "^(?=.*\\d+.*)(?=.*[A-Z]+.*)\\w{4,8}$";
    var pattern = Pattern.compile(password_pattern);
    var matcher = pattern.matcher("abc123");
    assertFalse(matcher.find());

    matcher = pattern.matcher("Aabc");
    assertFalse(matcher.find());

    matcher = pattern.matcher("Abc1xzy");
    assertTrue(matcher.find());

    // Negative Look Ahead
    pattern = Pattern.compile("(?!.*porn).*sex.*");
    matcher = pattern.matcher("my sex is female");
    assertTrue(matcher.find());

    matcher = pattern.matcher("Sex education can be taught in high school");
    assertFalse(matcher.find());

    matcher = pattern.matcher("hese are sex and porn websites");
    assertFalse(matcher.find());
}
```


