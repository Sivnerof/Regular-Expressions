# Regular Expressions

## Summary

I took this lesson from the [Regular Expressions](https://tryhackme.com/room/catregex "TryHackMe Regular Expressions") room on [TryHackMe](https://tryhackme.com/ "TryHackMe Website"). It was such a good lesson on regular expressions that I decided to put it into this repository so I can reference it later.

---

## Contents

* [Charsets](#charsets "Jump To Section")
* [Wildcards and Optional Characters](#wildcards-and-optional-characters "Jump To Section")
* [Metacharacters and Repetitions](#metacharacters-and-repetitions "Jump To Section")
* [Starts With, Ends With, Groups, and Either Or](#starts-with-ends-with-groups-and-either-of "Jump To Section")

---

## Charsets

When searching for a specific string in a file or block of text, you can search for it as is, with ```grep 'string' <file>``` . But what happens if you want to search for **patterns of text**? For example, you could be looking for a word that starts with a specific letter, or any words that end with numbers. That's where Regular Expressions come in.

Both of the aforementioned problems can be solved by using **charsets**. A charset is defined by enclosing in ```[``` square brackets ```]``` the character(s), or range of characters that you want to match.  Then, it finds **every occurrence** of the pattern you have defined in the file/text you are searching.

```[abc]``` will match ```a```, ```b```, and ```c``` (every occurrence of each letter).

```[abc]zz``` will match ```azz```, ```bzz```, and ```czz```.

You can also use a ```-``` dash to define ranges:
* ```[a-c]zz``` is the same as above.

And then you can combine ranges together:
* ```[a-cx-z]zz``` will match ```azz```, ```bzz```, ```czz```, ```xzz```, ```yzz```, and ```zzz```.

Most notably, this can be used to match any alphabetical character:
* ```[a-zA-Z]``` will match any **single** letter (lowercase or uppercase).

You can use numbers too:
* ```file[1-3]``` will match ```file1```, ```file2```, and ```file3```.

Then, there is a way to **exclude** characters from a charset with the ```^``` hat symbol, and include everything else.
```[^k]ing``` will match ```ring```, ```sing```, ```$ing```, but not ```king```.

Of course, you can exclude charsets, not just single characters.
```[^a-c]at``` will match ```fat``` and ```hat```, but not ```bat``` or ```cat```.

**NOTES**:

* Don't confuse strings with charsets. The charset ```[abc]``` will match the string ```abc```, but also ```cba``` and ```ca```. It doesn't match the string, but rather every occurrence of the specified characters in that string.

#### [BACK TO TOP](#regular-expressions "Jump To Top")

---

## Wildcards and Optional Characters

The wildcard that is used to match any single character (except the line break) is the ```.``` dot. That means that ```a.c``` will match ```aac```, ```abc```, ```a0c```, ```a!c```, and so on.

Also, you can set a character as optional in your pattern using the ```?``` question mark. That means that ```abc?``` will match ```ab``` and ```abc```, since the ```c``` is optional.

**NOTES**:

* If you want to search for ```.``` a literal dot, you have to **escape it** with a ```\``` reverse slash. That means that ```a.c``` will match ```a.c```, but also ```abc```, ```a@c```, and so on. But ```a\.c``` will match **just** ```a.c```.

#### [BACK TO TOP](#regular-expressions "Jump To Top")

---

## Metacharacters and Repetitions

There are easier ways to match bigger charsets. For example, ```\d``` is used to match any **single** digit. Here's a reference:

```\d``` matches a digit, like ```9```

```\D``` matches a non-digit, like ```A``` or ```@```

```\w``` matches an alphanumeric character, like ```a``` or ```3```

```\W``` matches a non-alphanumeric character, like ```!``` or ```#```

```\s``` matches a whitespace character (spaces, tabs, and line breaks)

```\S``` matches everything else (alphanumeric characters and symbols)

**Note**:

* Underscores ```_``` are included in the ```\w``` metacharacter and not in ```\W```. That means that ```\w``` will match every single character in ```test_file```.

Often we want a pattern that matches many characters of a single type in a row, and we can do that with repetitions. For example, ```{2}``` is used to match the preceding character (or metacharacter, or charset) two times in a row. That means that ```z{2}``` will match exactly ```zz```.

Here's a reference for each repetition along with how many times it matches the preceding pattern:

```{12}``` - **exactly** 12 times.

```{1,5}``` - **1 to 5** times.

```{2,}``` - **2 or more** times.

```*``` - **0 or more** times.

```+``` - **1 or more** times.

#### [BACK TO TOP](#regular-expressions "Jump To Top")

---

## Starts With, Ends With, Groups, and Either Of


Sometimes it's very useful to specify that we want to search by a certain pattern **in the beginning or the end of a line**. We do that with these characters:

```^``` - starts with

```$``` - ends with

So for example, if you want to search for a line that **starts with** ```abc```, you can use ```^abc```.

If you want to search for a line that **ends with** ```xyz```, you can use ```xyz$```.

**NOTES**:

* The ```^``` hat symbol is used to exclude a charset when enclosed in ```[```square brackets```]```, but when it is not, it is used to specify the beginning of a word.

* You can also define groups by enclosing a pattern in ```(```parentheses```)```. This function can be used for many ways that are not in the scope of this tutorial. We will use it to define an **either/or** pattern, and also to repeat patterns. To say "or" in Regex, we use the ```|``` pipe.

* For an "either/or" pattern example, the pattern ```during the (day|night)``` will match both of these sentences: ```during the day``` and ```during the night```.

* For a repetition example, the pattern ```(no){5}``` will match the sentence ```nonononono```.

---

#### [BACK TO TOP](#regular-expressions "Jump To Top")