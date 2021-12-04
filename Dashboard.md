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
const musicsWithoutSheet = dv.pages('"Músicas"')
	.where(page => {
		if (!page.Partituras) return true;
		if (Array.isArray(page.Partituras)) {
			return page.Partituras.values.length === 0;
		}
		return 
		console.log({ partituras: page.Partituras })
		return !page.Partituras.values || page.Partituras.values.length === 0
	})

dv.list(musicsWithoutSheet.file.link)
```

# Músicas sem gravações
```dataviewjs
const musicsWithoutRecordings = dv.pages('"Músicas"')
	.where(page => !page.Gravações.values || page.Gravações.values.length === 0)

dv.list(musicsWithoutRecordings.file.link)
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