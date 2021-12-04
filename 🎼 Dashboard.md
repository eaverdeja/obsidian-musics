# 🎼 Dashboard

## Repertório Eduardo Verdeja

```dataviewjs
for(let group of dv.pages('"🤓 Repertórios/Eduardo Verdeja"').groupBy(p => p.Domínio)) {
	dv.header("3", group.key)
	dv.table(["Música", "Tonalidade", "Instrumento"],
        group.rows
			.sort(k => k.Música)
            .map(k => [
				k.Música,
				k.Tonalidade,
				k.Instrumento,
			]
		)
	)
}
```

---

## Repertório Philip Lonergan

```dataviewjs
for(let group of dv.pages('"🤓 Repertórios/Philip Lonergan"').groupBy(p => p.file.link)) {
	dv.header("3", group.key)
	dv.el("p", group.rows.map(r => r.file.outlinks))
}
```

---

## Músicas por ritmo

```dataviewjs
for (let group of dv.pages('"🎶 Músicas"').groupBy(p => p.Ritmos)) {
    dv.header(3, group.key);
	dv.el("p", `This category has ${group.rows.length} songs`)
    dv.table(["Música", "Compositores", "Intérpretes", "Partituras"],
        group.rows
			.sort(k => k.file.link)
            .map(k => [
				k.file.link,
				k.Compositores,
				k.Intérpretes,
				k.Partituras
			]
		)
	)
}
```

---

## Músicas sem partitura
```dataviewjs
const musicsWithoutSheet = dv.pages('"🎶 Músicas"')
	.where(page => {
		const sheets = page.Partituras;
		if (!sheets) return true;
		if (sheets.values && Array.isArray(sheets.values)) {
			return sheets.values.length === 0;
		}
		return !sheets;
	})

dv.list(musicsWithoutSheet.file.link)
```

---

## Músicas sem gravações
```dataviewjs
const musicsWithoutRecordings = dv.pages('"🎶 Músicas"')
	.where(page => {
		const recordings = page.Gravações
		if (!recordings) return true;
		if (recordings.values && Array.isArray(recordings.values)) {
			return recordings.values.length === 0;
		}
		return !recordings;
	})

dv.list(musicsWithoutRecordings.file.link)
```
