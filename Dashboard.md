# Músicas por ritmo

```dataviewjs
for (let group of dv.pages('"Músicas"').groupBy(p => p.Ritmos)) {
    dv.header(3, group.key);
    dv.table(["Música", "Compositores", "Intérpretes", "Gravações", "Partituras"],
        group.rows
            .map(k => [
				k.file.link,
				k.Compositores,
				k.Intérpretes,
				k.Gravações,
				k.Partituras
			]
		)
	)
}
```

# Músicas sem partitura
```dataviewjs
const musicsWithoutSheet = dv.pages("")
```

# Níveis de estudo Verdeja
```dataviewjs
for(let group of dv.pages('"Repertórios/Eduardo Verdeja-*"').groupBy(p => p.file.link)) {
	dv.header("3", group.key)
	dv.el("p", group.rows.map(r => r.file.outlinks))
}
```

# Níveis de estudo Phil

```dataviewjs
for(let group of dv.pages('"Repertórios/Philip Lonergan"').groupBy(p => p.file.link)) {
	dv.header("3", group.key)
	dv.el("p", group.rows.map(r => r.file.outlinks))
}
```