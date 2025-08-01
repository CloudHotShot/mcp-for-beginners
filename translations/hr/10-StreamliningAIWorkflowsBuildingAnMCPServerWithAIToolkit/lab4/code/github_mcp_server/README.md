<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a3f252a62f059360855de5331a575898",
  "translation_date": "2025-07-14T09:04:12+00:00",
  "source_file": "10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/README.md",
  "language_code": "hr"
}
-->
# Weather MCP Server

Ovo je primjer MCP Servera u Pythonu koji implementira alate za vremensku prognozu s lažnim odgovorima. Može se koristiti kao osnova za vlastiti MCP Server. Uključuje sljedeće značajke:

- **Weather Tool**: alat koji pruža lažne informacije o vremenu na temelju zadane lokacije.
- **Git Clone Tool**: alat koji klonira git repozitorij u određenu mapu.
- **VS Code Open Tool**: alat koji otvara mapu u VS Code ili VS Code Insiders.
- **Connect to Agent Builder**: značajka koja omogućuje povezivanje MCP servera s Agent Builderom za testiranje i otklanjanje pogrešaka.
- **Debug in [MCP Inspector](https://github.com/modelcontextprotocol/inspector)**: značajka koja omogućuje otklanjanje pogrešaka MCP Servera pomoću MCP Inspectora.

## Početak rada s Weather MCP Server predloškom

> **Preduvjeti**
>
> Za pokretanje MCP Servera na vašem lokalnom razvojnom računalu trebat će vam:
>
> - [Python](https://www.python.org/)
> - [Git](https://git-scm.com/) (potrebno za git_clone_repo alat)
> - [VS Code](https://code.visualstudio.com/) ili [VS Code Insiders](https://code.visualstudio.com/insiders/) (potrebno za open_in_vscode alat)
> - (*Opcionalno - ako preferirate uv*) [uv](https://github.com/astral-sh/uv)
> - [Python Debugger Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.debugpy)

## Priprema okruženja

Postoje dva pristupa za postavljanje okruženja za ovaj projekt. Možete odabrati onaj koji vam više odgovara.

> Napomena: Ponovno učitajte VSCode ili terminal kako biste osigurali da se koristi python iz virtualnog okruženja nakon što ga kreirate.

| Pristup | Koraci |
| -------- | ----- |
| Korištenje `uv` | 1. Kreirajte virtualno okruženje: `uv venv` <br>2. Pokrenite VSCode naredbu "***Python: Select Interpreter***" i odaberite python iz kreiranog virtualnog okruženja <br>3. Instalirajte ovisnosti (uključujući razvojne): `uv pip install -r pyproject.toml --extra dev` |
| Korištenje `pip` | 1. Kreirajte virtualno okruženje: `python -m venv .venv` <br>2. Pokrenite VSCode naredbu "***Python: Select Interpreter***" i odaberite python iz kreiranog virtualnog okruženja<br>3. Instalirajte ovisnosti (uključujući razvojne): `pip install -e .[dev]` |

Nakon postavljanja okruženja, možete pokrenuti server na svom lokalnom razvojnom računalu putem Agent Buildera kao MCP Klijenta za početak rada:
1. Otvorite VS Code Debug panel. Odaberite `Debug in Agent Builder` ili pritisnite `F5` za pokretanje otklanjanja pogrešaka MCP servera.
2. Koristite AI Toolkit Agent Builder za testiranje servera s [ovim promptom](../../../../../../../../../../open_prompt_builder). Server će se automatski povezati s Agent Builderom.
3. Kliknite `Run` za testiranje servera s promptom.

**Čestitamo**! Uspješno ste pokrenuli Weather MCP Server na svom lokalnom razvojnom računalu putem Agent Buildera kao MCP Klijenta.  
![DebugMCP](https://raw.githubusercontent.com/microsoft/windows-ai-studio-templates/refs/heads/dev/mcpServers/mcp_debug.gif)

## Što je uključeno u predložak

| Mapa / Datoteka | Sadržaj                                     |
| --------------- | -------------------------------------------- |
| `.vscode`       | VSCode datoteke za otklanjanje pogrešaka    |
| `.aitk`         | Konfiguracije za AI Toolkit                   |
| `src`           | Izvorni kod za weather mcp server             |

## Kako otkloniti pogreške u Weather MCP Serveru

> Napomene:
> - [MCP Inspector](https://github.com/modelcontextprotocol/inspector) je vizualni alat za razvojne programere za testiranje i otklanjanje pogrešaka MCP servera.
> - Svi načini otklanjanja pogrešaka podržavaju prekide (breakpoints), tako da možete dodavati prekide u kod implementacije alata.

## Dostupni alati

### Weather Tool  
`get_weather` alat pruža lažne informacije o vremenu za zadanu lokaciju.

| Parametar | Tip | Opis |
| --------- | --- | ----- |
| `location` | string | Lokacija za koju se traži vremenska prognoza (npr. ime grada, država ili koordinate) |

### Git Clone Tool  
`git_clone_repo` alat klonira git repozitorij u zadanu mapu.

| Parametar | Tip | Opis |
| --------- | --- | ----- |
| `repo_url` | string | URL git repozitorija koji se klonira |
| `target_folder` | string | Putanja do mape u koju treba klonirati repozitorij |

Alat vraća JSON objekt s:  
- `success`: Boolean koji označava je li operacija bila uspješna  
- `target_folder` ili `error`: Putanja kloniranog repozitorija ili poruka o pogrešci

### VS Code Open Tool  
`open_in_vscode` alat otvara mapu u VS Code ili VS Code Insiders aplikaciji.

| Parametar | Tip | Opis |
| --------- | --- | ----- |
| `folder_path` | string | Putanja do mape koju treba otvoriti |
| `use_insiders` | boolean (opcionalno) | Koristiti li VS Code Insiders umjesto redovnog VS Codea |

Alat vraća JSON objekt s:  
- `success`: Boolean koji označava je li operacija bila uspješna  
- `message` ili `error`: Potvrdna poruka ili poruka o pogrešci

## Debug Mode | Opis | Koraci za otklanjanje pogrešaka |
| ---------- | ----------- | --------------- |
| Agent Builder | Otklanjanje pogrešaka MCP servera u Agent Builderu putem AI Toolkit-a. | 1. Otvorite VS Code Debug panel. Odaberite `Debug in Agent Builder` i pritisnite `F5` za pokretanje otklanjanja pogrešaka MCP servera.<br>2. Koristite AI Toolkit Agent Builder za testiranje servera s [ovim promptom](../../../../../../../../../../open_prompt_builder). Server će se automatski povezati s Agent Builderom.<br>3. Kliknite `Run` za testiranje servera s promptom. |
| MCP Inspector | Otklanjanje pogrešaka MCP servera pomoću MCP Inspectora. | 1. Instalirajte [Node.js](https://nodejs.org/)<br> 2. Postavite Inspector: `cd inspector` && `npm install` <br> 3. Otvorite VS Code Debug panel. Odaberite `Debug SSE in Inspector (Edge)` ili `Debug SSE in Inspector (Chrome)`. Pritisnite F5 za početak otklanjanja pogrešaka.<br> 4. Kada se MCP Inspector pokrene u pregledniku, kliknite gumb `Connect` za povezivanje ovog MCP servera.<br> 5. Zatim možete `List Tools`, odabrati alat, unijeti parametre i `Run Tool` za otklanjanje pogrešaka u kodu servera.<br> |

## Zadani portovi i prilagodbe

| Debug Mode | Portovi | Definicije | Prilagodbe | Napomena |
| ---------- | ------- | ---------- | ---------- | -------- |
| Agent Builder | 3001 | [tasks.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/tasks.json) | Uredite [launch.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/launch.json), [tasks.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/tasks.json), [\_\_init\_\_.py](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/src/__init__.py), [mcp.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.aitk/mcp.json) za promjenu navedenih portova. | N/A |
| MCP Inspector | 3001 (Server); 5173 i 3000 (Inspector) | [tasks.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/tasks.json) | Uredite [launch.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/launch.json), [tasks.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.vscode/tasks.json), [\_\_init\_\_.py](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/src/__init__.py), [mcp.json](../../../../../../10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/lab4/code/github_mcp_server/.aitk/mcp.json) za promjenu navedenih portova. | N/A |

## Povratne informacije

Ako imate bilo kakve povratne informacije ili prijedloge za ovaj predložak, molimo otvorite issue na [AI Toolkit GitHub repozitoriju](https://github.com/microsoft/vscode-ai-toolkit/issues)

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden korištenjem AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako težimo točnosti, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati službenim i autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni ljudski prijevod. Ne snosimo odgovornost za bilo kakve nesporazume ili pogrešne interpretacije koje proizlaze iz korištenja ovog prijevoda.