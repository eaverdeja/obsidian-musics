# 🎼 Dashboard

## Repertório Eduardo Verdeja
```dataviewjs
const order = ["💪 Domínio Grande", "👍 Domínio Médio", "🙇‍♂️ Domínio Pequeno"]
const repertoire = dv.pages('"🤓 Repertórios/Eduardo Verdeja"')

const repertoireBySkill = repertoire
	.groupBy(r => r.Domínio)
	.array()
	.sort((a, b) => {
		return order.indexOf(a.key.path) - order.indexOf(b.key.path)
	})

for(let skillGroup of repertoireBySkill.sort(g => g.instrumento)) {
	dv.header("3", skillGroup.key)
	dv.table(["Música", "Tonalidade", "Instrumento"],
        skillGroup.rows
			.sort(k => [k.Instrumento, k.Música])
            .map(k => [
				k.Música,
				k.Tonalidade,
				k.Instrumento,
			]
		)
	)
}

const repertoireByTonality = repertoire.groupBy(r => r.Tonalidade).sort(g => g.rows.values.length, "desc")

for(let tonalityGroup of repertoireByTonality) {
	console.log({tonalityGroup})
	dv.el("p", `Você tem ${tonalityGroup.rows.values.length} músicas em ${tonalityGroup.key.path} no seu repertório`)
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
