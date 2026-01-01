
# Temps


Find out when this web app was compiled. Report your answer as a Unix timestamp in milliseconds wrapped with `bcactf{}`. (For example, the date "Wed, 01 Jan 2020 05:00:00 GMT" would be reported as `bcactf{1577854800000}`)
[http://challs.bcactf.com:26137](http://challs.bcactf.com:26137/)
## Solucion

- En el código encontramos un js que nos da ese dato

- salto 1
- 
http://challs.bcactf.com:26137/

```html



<script>
				{
					__sveltekit_1kkkrww = {
						base: new URL(".", location).pathname.slice(0, -1)
					};

					const element = document.currentScript.parentElement;

					Promise.all([
						import("./_app/immutable/entry/start.DkKzmX4k.js"),
						import("./_app/immutable/entry/app.Sx03DtkF.js")
					]).then(([kit, app]) => {
						kit.start(app, element, {
							node_ids: [0, 2],
							data: [null,null],
							form: null,
							error: null
						});
					});
				}
			</script>


```

- salto 2
http://challs.bcactf.com:26137/_app/immutable/entry/start.DkKzmX4k.js
```


import{a as t}from"../chunks/entry.Cv3YAutr.js";export{t as start};
```


- salto 3
http://challs.bcactf.com:26137/_app/immutable/chunks/entry.Cv3YAutr.js

```


const en = ((oe = globalThis.__sveltekit_1kkkrww) == null ? void 0 : oe.assets) ?? x,
    nn = "1735776187591",
    ue = "sveltekit:snapshot",
    he = "sveltekit:scroll",
    de = "sveltekit:states",
    rn = "sveltekit:pageurl",
    G = "sveltekit:history",
    J = "sveltekit:navigation",
    ut = {
        tap: 1,
        hover: 2,
        viewport: 3,
        eager: 4,
        off: -1,
        false: -1
    },
    ft = location.origin;

```




```




bcactf{1735776187591}
```