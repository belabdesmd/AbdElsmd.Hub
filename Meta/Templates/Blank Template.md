---
date: <%*tR += tp.date.now("YYYY-MM-DD") + "\n"%>
<%*
	const folder = tp.file.path();
	if (folder.contains("Nomos")) {
		tR += "cssclasses: [page, red]";
	} else if (folder.contains("Gnosis")) {
		tR += "cssclasses: [page, orange]";
	} else if (folder.contains("Techne")) {
		tR += "cssclasses: [page, yellow]";
	} else if (folder.contains("Osmosis")) {
		tR += "cssclasses: [page, tangerine]";
	} else if (folder.contains("Religion")) {
		tR += "cssclasses: [page, green]";
	}
%>
---
<%*
if (folder.contains("Daily")) {
    tR += `# _${tp.date.now("dddd DD MMM, YYYY")}_\n\n - `;
}
%>