# 🎼 Dashboard

## Repertório Eduardo Verdeja
```dataviewjs
const order = ["💪 Domínio Grande", "👍 Domínio Médio", "🙇‍♂️ Domínio Pequeno"]
const repertoire = dv.pages('"🤓 Repertórios/Eduardo Verdeja"')

const repertoireBySkill = repertoire
	.groupBy(r => r.Domínio)
	.array()
	.sort((a, b) => {
		// (a or b).key.path is 💪 Domínio Grande or 👍 Domínio Médio etc.
		return order.indexOf(a.key.path) - order.indexOf(b.key.path)
	})
for(let skillGroup of repertoireBySkill.sort(g => g.Instrumento)) {
	dv.header("5", skillGroup.key)
	dv.table(["Música/Instrumento", "Tonalidades"],
        skillGroup.rows
			.sort(k => [k.Instrumento, k.Música])
            .map(k => [
				k.file.link,
				k.Tonalidade,
			]
		)
	)
}

dv.el("hr", "")
dv.header("3", "Quantidade de músicas/tonalidade")
const repertoireByTonality = repertoire
	.groupBy(r => r.Tonalidade)
	.sort(g => g.rows.values.length, "desc")
for(let tonalityGroup of repertoireByTonality) {
	dv.el("p", `Você tem ${tonalityGroup.rows.values.length} músicas em ${tonalityGroup.key} no seu repertório`)	
}

dv.el("hr", "")
dv.header("3", "Quantidade de músicas/instrumento")
const repertoireByInstrument = repertoire
	.groupBy(r => r.Instrumento)
	.sort(g => g.rows.values.length, "desc")
for(let instrumentGroup of repertoireByInstrument) {
	dv.el("p", `Você tem ${instrumentGroup.rows.values.length} músicas tocadas no  ${instrumentGroup.key} no seu repertório`)
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
    dv.table(["Música", "Compositores", "Intérpretes", "Tonalidades"],
        group.rows
			.sort(k => k.file.link)
            .map(k => [
				k.file.link,
				k.Compositores,
				k.Intérpretes,
				k.Tonalidades,
			]
		)
	)
}
```

---

## Músicas sem partitura
```dataviewjs
const songsWithoutSheet = dv.pages('"🎶 Músicas"')
	.where(page => {
		const sheets = page.Partituras;
		if (!sheets) return true;
		if (sheets.values) {
			return sheets.values.length === 0;
		}
		return !sheets;
	})

dv.list(songsWithoutSheet.file.link)
```

---

## Músicas sem gravações
```dataviewjs
const songsWithoutRecordings = dv.pages('"🎶 Músicas"')
	.where(page => {
		const recordings = page.Gravações
		if (!recordings) return true;
		if (recordings.values) {
			return recordings.values.length === 0;
		}
		return !recordings;
	})

dv.list(songsWithoutRecordings.file.link)
```
