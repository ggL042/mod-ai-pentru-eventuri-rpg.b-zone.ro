# BZone Events Windows 1.1.0

Un singur modul Lua pentru **evenimente SMS**: copiere de text și întrebări/trivia. 

## Instalare pe Windows, pas cu pas

Ghid pentru GTA San Andreas clasic pe PC, SA:MP și Windows 10/11. Dacă ai deja SA:MP și MoonLoader funcționale, verifică bibliotecile de la pasul 4 și continuă cu instalarea modulului.

### 1. GTA San Andreas și SA:MP

1. Folosește o instalare GTA San Andreas clasic compatibilă cu SA:MP; acest pachet nu este pentru Definitive Edition.
2. Deschide [pagina B-Zone](https://www.b-zone.ro/) și folosește descărcarea din secțiunea **Instalează SA-MP**.
3. La instalarea clientului selectează folderul care conține `gta_sa.exe`, de exemplu `C:\Games\GTA San Andreas`. Acesta este „folderul jocului” în pașii următori.
4. Pornește `samp.exe`, setează numele jucătorului și adaugă la favorite `rpg.b-zone.ro`.
5. Intră o dată pe server înainte de instalarea modurilor, pentru a verifica jocul de bază.

Versiunea clientului trebuie să fie compatibilă și cu SAMPFUNCS ales la pasul 3. Nu presupune că toate reviziile SA:MP sunt interschimbabile; verifică cerințele pachetului SAMPFUNCS înainte de instalare.

### 2. ASI Loader și MoonLoader

MoonLoader încarcă fișierele Lua în joc. Pentru încărcarea fișierului `moonloader.asi` ai nevoie de un ASI Loader.

- [MoonLoader — pagina proiectului](https://www.blast.hk/moonloader/)
- [MoonLoader — topic de descărcare](https://www.blast.hk/threads/13305/)
- [Ultimate ASI Loader — descărcări oficiale](https://github.com/ThirteenAG/Ultimate-ASI-Loader/releases)

1. Închide jocul.
2. Dacă ai deja un ASI Loader funcțional, păstrează-l. Dacă lipsește, descarcă varianta **Win32/x86** a Ultimate ASI Loader: GTA SA este un proces pe 32 de biți, chiar pe Windows pe 64 de biți. Extrage `dinput8.dll` lângă `gta_sa.exe`. Păstrează o copie a fișierului existent dacă există deja unul cu acest nume.
3. Instalează MoonLoader în același folder al jocului, urmând instrucțiunile pachetului. Pentru o arhivă, copiază conținutul destinat jocului, inclusiv `moonloader.asi` și folderul `moonloader`, păstrând structura.
4. Păstrează bibliotecile standard incluse în distribuția MoonLoader. Simpla creare a unui folder gol numit `moonloader` nu instalează MoonLoader.

Paginile BlastHack nu au putut fi deschise automat la redactarea acestui ghid. Linkurile sunt incluse pentru acces din browser; versiunea și disponibilitatea atașamentelor trebuie verificate pe pagină.

### 3. SAMPFUNCS

**Este necesar pentru versiunea SAMP.Lua indicată aici.** Biblioteca verifică explicit existența lui la încărcare: [verificarea din codul SAMP.Events](https://github.com/THE-FYP/SAMP.Lua/blob/master/samp/events/core.lua).

1. Deschide [topic-ul SAMPFUNCS de pe BlastHack](https://www.blast.hk/threads/17/).
2. Alege pachetul compatibil cu revizia SA:MP instalată, conform instrucțiunilor autorului.
3. Copiază `SAMPFUNCS.asi` lângă `gta_sa.exe`, împreună cu celelalte fișiere/foldere din pachet, în locațiile indicate de acesta.
4. Nu pune `SAMPFUNCS.asi` în `moonloader/lib`.

### 4. Biblioteca SAMP.Lua

Descarcă din [depozitul oficial THE-FYP/SAMP.Lua](https://github.com/THE-FYP/SAMP.Lua): **Code → Download ZIP**.

1. Dezarhivează pachetul.
2. Din interiorul lui, copiază **întregul folder `samp`** în `moonloader/lib`.
3. Verifică să existe `moonloader/lib/samp/events.lua` și subfolderul `moonloader/lib/samp/events`.

Nu copia numai `events.lua` și nu lăsa un nivel suplimentar precum `lib/SAMP.Lua-master/samp`. [Instrucțiunile autorului](https://github.com/THE-FYP/SAMP.Lua#installation) cer întregul folder `samp`.

Modulul folosește și `ffi` din LuaJIT și funcțiile JSON incluse în MoonLoader. Nu trebuie instalate separat Python, Node.js, Lua, LuaRocks, `requests`, `effil`, `mimgui`, Chromium sau librăriile vechiului bot.

### 5. Verificarea curl

În Windows 10/11, curl este de regulă deja inclus. [Documentația Microsoft](https://learn.microsoft.com/en-us/windows/curl/) descrie utilitarul integrat.

Deschide **Command Prompt / CMD** și execută:

```bat
%SystemRoot%\System32\curl.exe --version
```

Dacă apare versiunea, verificarea este reușită și poți continua. Folosește `curl.exe`, pentru a evita confuzia cu aliasul `curl` din unele versiuni PowerShell.

**Dacă lipsește:**

1. Deschide [descărcările oficiale curl pentru Windows](https://curl.se/windows/).
2. Pentru Windows pe 64 de biți cu procesor Intel/AMD, descarcă pachetul **x64**. curl rulează separat de joc, deci poate fi pe 64 de biți.
3. Dezarhivează și copiază `curl.exe` din directorul `bin` în `moonloader/lib/curl.exe`. Păstrează alături eventualele fișiere de suport din `bin`, inclusiv certificatul CA dacă pachetul îl conține.
4. Verifică din CMD, adaptând calea la joc:

```bat
"C:\Games\GTA San Andreas\moonloader\lib\curl.exe" --version
```

Modulul caută, în această ordine, `Windows\Sysnative\curl.exe`, `Windows\System32\curl.exe`, apoi `moonloader\lib\curl.exe`. Nu caută în toate directoarele din PATH. `Sysnative` este folosit de procesul jocului pe 32 de biți pentru a accesa utilitarul Windows pe 64 de biți; nu trebuie creat manual.

O copie din `moonloader/lib` este folosită numai dacă nu este găsit curl în Windows. Dacă varianta Windows există dar nu funcționează, simpla adăugare a copiei locale nu schimbă prioritatea.

### 6. Instalarea botului

1. Dezarhivează `BZoneEvents_Windows.zip`.
2. Copiază `BZoneEvents_Windows.lua` direct în folderul `moonloader` al jocului.
3. Mută vechiul bot și eventualele copii ale lui în afara folderului `moonloader`, pentru a evita comenzile și SMS-urile duble.
4. Repornește jocul.

Structura relevantă trebuie să arate astfel; fișierele suplimentare ale MoonLoader/SAMPFUNCS rămân la locul lor:

```text
GTA San Andreas/
├── gta_sa.exe
├── samp.exe
├── samp.dll
├── dinput8.dll                  ← dacă folosești acest ASI Loader
├── moonloader.asi
├── SAMPFUNCS.asi
└── moonloader/
    ├── BZoneEvents_Windows.lua
    ├── BZoneEvents_AI.json      ← apare după salvarea configurației
    └── lib/
        ├── samp/
        │   ├── events.lua
        │   ├── events/
        │   └── ...             ← restul bibliotecii SAMP.Lua
        └── curl.exe            ← opțional, dacă lipsește cel din Windows
```

### 7. Prima pornire și cheia AI

1. Intră pe server și scrie `/aistatus`. Trebuie să apară starea evenimentelor, furnizorul și modelul.
2. Modulul pornește cu evenimentele **ON**. `/aievents` comută starea; verifică din nou cu `/aistatus`.
3. Pentru schimbarea cheii, copiază cheia API completă în clipboard și folosește comanda corespunzătoare de mai jos.

| Serviciu | Pagina pentru cont/cheie | Comandă în joc după copierea cheii |
| --- | --- | --- |
| Groq | [Groq Console](https://console.groq.com/keys) | `/aikey groq` |
| OpenAI | [OpenAI API keys](https://platform.openai.com/api-keys) | `/aikey openai` |
| Claude | [Anthropic Console](https://console.anthropic.com/) | `/aikey claude` |

Ai nevoie de acces API pentru modelul ales și de cotă disponibilă în cont. Nu introduce parola contului sau cookie-uri. Pachetul păstrează o singură cheie Groq inițială; nu rotește chei și nu schimbă automat furnizorul după erori.

Copierea textelor de eveniment funcționează fără cerere AI. Trivia necesită serviciul AI configurat. Pentru trimitere trebuie să poți folosi `/sms` în joc; modulul nu cumpără telefon și nu elimină restricțiile serverului. Cele **150 ms** se adaugă după pregătirea răspunsului, separat de timpul de răspuns al AI-ului.

### 8. Opțional: AI local

Alege una dintre variante; nu ai nevoie de ambele pentru bot.

**Ollama**

1. Instalează din [Ollama pentru Windows](https://ollama.com/download/windows).
2. Pornește aplicația și descarcă un model de conversație din [biblioteca Ollama](https://ollama.com/library), potrivit calculatorului tău.
3. În CMD, `ollama list` arată numele modelelor instalate. Folosește numele exact în `/aikey ollama NUME_MODEL`.
4. Păstrează Ollama pornit. Serverul implicit folosește portul `11434`. [Ghidul oficial Windows](https://docs.ollama.com/windows).

**LM Studio**

1. Instalează [LM Studio](https://lmstudio.ai/download).
2. Descarcă și încarcă un model de conversație.
3. În fila **Developer**, pornește serverul local și verifică portul, implicit `1234` pentru configurația botului.
4. În joc: `/aikey lmstudio NUME_MODEL`, folosind identificatorul modelului expus de server. [Ghidul oficial al serverului](https://lmstudio.ai/docs/developer/core/server).

Modelele locale trebuie să poată returna răspunsul JSON cerut de modul. Prima încărcare poate dura; încarcă modelul înainte de eveniment. Performanța depinde de model și calculator, iar rularea locală consumă resurse împreună cu jocul.

### 9. Probleme frecvente

| Problemă | Ce verifici |
| --- | --- |
| `/aistatus` este comandă necunoscută | Scriptul trebuie să fie în folderul `moonloader` al jocului pornit, cu extensia `.lua`, nu `.lua.txt`. Verifică `moonloader/moonloader.log`. |
| Nu apare niciun jurnal MoonLoader după pornire | Verifică încărcarea ASI Loader și existența `moonloader.asi` lângă `gta_sa.exe`. |
| `module 'lib.samp.events' not found` | Copiază întregul folder `samp` în `moonloader/lib`; verifică nivelurile de directoare. |
| `samp.events requires SAMPFUNCS` | Instalează/încarcă SAMPFUNCS compatibil cu versiunea SA:MP. |
| Lipsesc `ffi`, `encodeJson` sau `decodeJson` | Verifică instalarea completă MoonLoader/LuaJIT; nu folosi un interpretor Lua separat. |
| `curl.exe indisponibil` | Urmează pasul 5. Verifică și că Windows permite crearea fișierelor în folderul temporar al utilizatorului. |
| Windows nu poate porni curl | Rulează manual acel `curl.exe --version`; verifică arhitectura și fișierele lui de suport. |
| Eroare de autentificare / HTTP 401 | Copiază din nou cheia completă și selectează furnizorul corect cu `/aikey`. |
| HTTP 429 | Verifică limita/cota contului; modulul nu trece automat la altă cheie. |
| Model inexistent sau inaccesibil | Folosește `/aikey model NUME_MODEL` cu un model disponibil în contul/serviciul ales. |
| Conexiunea locală eșuează | Pornește serverul, încarcă modelul și verifică portul. Vezi comenzile de mai jos pentru alt port. |
| Configurația nu se salvează | Folderul `moonloader` trebuie să permită scrierea fișierului `BZoneEvents_AI.json`; altfel modificarea rămâne numai pentru sesiunea curentă. |
| Copiază texte, dar nu răspunde la trivia | Verifică cheia, curl, modelul și mesajele de eroare AI. Copierea nu folosește rețeaua. |
| Nu răspunde când scrii tu o întrebare în chat | Modulul urmărește anunțurile de eveniment recunoscute, nu chatul obișnuit. |
| Trimite de două ori | Verifică dacă ai păstrat activ și botul vechi sau două copii ale noului script. |

Pentru diagnostic, păstrează mesajul exact și liniile relevante din `moonloader/moonloader.log`. Nu include cheile API sau fișierul de configurare cu cheia în raport.

## Cele trei comenzi

| Comandă | Efect |
| --- | --- |
| `/aievents` | Comută ON/OFF; OFF anulează și răspunsurile în așteptare |
| `/aistatus` | Arată ON/OFF, furnizorul și modelul activ; nu afișează cheia |
| `/aikey` | Configurează cheia, furnizorul sau modelul, conform exemplelor de mai jos |

### Cheie copiată în clipboard

**Copiază cheia API completă**, apoi scrie în joc una dintre comenzile:

```text
/aikey groq
/aikey openai
/aikey claude
```

Această variantă funcționează și pentru chei mai lungi decât limita chatului SA:MP. `/aikey` fără argumente încearcă să recunoască furnizorul din prefixul cheii copiate: `gsk_` → Groq, `sk-ant-` → Claude, `sk-` → OpenAI. Se folosesc chei API ale serviciilor, nu cookie-uri sau date de autentificare ChatGPT/Claude din browser.

Poți lipi și cheia direct, dacă încape integral în chat:

```text
/aikey CHEIA_COMPLETA
/aikey groq CHEIA_COMPLETA
/aikey openai CHEIA_COMPLETA
/aikey claude CHEIA_COMPLETA
```

Opțional, la forma cu furnizor explicit poți adăuga modelul după cheie. Aliasurile `chatgpt` și `anthropic` sunt acceptate pentru `openai` și `claude`.

### Modele locale

Pornește serverul Ollama sau LM Studio pe calculatorul Windows și instalează/încarcă modelul dorit. Modulul nu descarcă modele și nu pornește serverul în locul tău.

```text
/aikey local NUMELE_MODELULUI_INSTALAT
/aikey lmstudio NUMELE_MODELULUI_INCARCAT
```

`local` este alias pentru `ollama`. În mod implicit, local nu folosește nicio cheie și nu trimite cheia cloud anterioară. Dacă ai activat autentificarea serverului local, adaugă tokenul după numele modelului.

Adrese implicite:

- Ollama: `http://127.0.0.1:11434/v1/chat/completions`
- LM Studio: `http://127.0.0.1:1234/v1/chat/completions`

Pentru alt port, după selectarea furnizorului local:

```text
/aikey url http://127.0.0.1:9000
```

Sunt acceptate adrese locale `127.0.0.1` sau `localhost`, cu port explicit. Modelele locale trebuie să suporte conversații și răspunsuri JSON; răspunsurile incomplete sau invalide nu sunt trimise ca SMS.

### Schimbarea modelului

```text
/aikey model NUMELE_MODELULUI
/aikey help
```

Schimbarea modelului păstrează cheia și furnizorul activ. Alege un model accesibil contului tău și compatibil cu API-ul folosit.

| Furnizor | Model implicit | API |
| --- | --- | --- |
| Groq | `llama-3.3-70b-versatile` | Chat Completions |
| OpenAI | `gpt-4.1-mini` | Chat Completions |
| Claude | `claude-haiku-4-5` | Anthropic Messages |
| Ollama / LM Studio | Specificat de tine | Chat Completions local |

## Salvarea configurației

Cheia, furnizorul, modelul și adresa locală sunt salvate în `moonloader/BZoneEvents_AI.json` și încărcate la următoarea pornire. Există **o singură configurație activă**. Schimbarea ei anulează cererile și SMS-urile încă netrimise. Confirmarea salvării nu înseamnă că cheia a fost verificată printr-un apel plătit; verificarea serviciului are loc la următoarea întrebare de eveniment.

Dacă salvarea eșuează, mesajul indică faptul că schimbarea rămâne valabilă numai pentru sesiunea curentă. Un fișier de configurare invalid dezactivează cererile AI până la reconfigurare; copierea textelor rămâne disponibilă.

**Fișierul Lua conține cheia Groq inițială, iar configurația salvată poate conține cheia nouă. Păstrează aceste fișiere private.**

## Comportamentul la evenimente

- Recunoaște organizator Eveniment și Helper, `T:`, `Text:` și formulări precum `Primul care mi trimite "kqbwdyiuqddqd" castiga`.
- Copierea textului nu consumă API. Majusculele și punctuația sunt păstrate.
- Destinatarul este cel indicat prin `/sms` sau printr-o formulare cu ID; altfel, organizatorul.
- Nu trimite răspunsuri duplicate, anulate sau din runde încheiate. Nu trunchiază textele care depășesc limita unui SMS.
- Nu răspunde prin SMS la cereri de whisper și ignoră chatul obișnuit.
- Cererile rulează separat prin `curl.exe`; fără așteptare de rețea blocantă în chat.
- Nu are telefon, clan, WT, wiki sau login web.

## Verificări și limite

Compilarea LuaJIT/Lua 5.1 și **86 de verificări offline** au trecut: evenimentele, +150 ms pentru copiere/AI, anularea răspunsurilor, cheia copiată lungă, salvarea/reîncărcarea, formatele de autentificare și răspuns Claude/OpenAI/Groq/local, lipsa cheii cloud în cererile locale și erorile de configurare.

API-urile au fost simulate în teste. Nu au fost efectuate apeluri plătite și modulul nu a fost rulat efectiv în GTA pe Windows. Nu înseamnă compatibilitate universală cu orice serviciu sau orice model: sunt implementate cele cinci variante de mai sus.

Documentație folosită: [OpenAI Chat Completions](https://developers.openai.com/api/reference/resources/chat), [GPT-4.1 mini](https://developers.openai.com/api/docs/models/gpt-4.1-mini), [Anthropic Messages](https://platform.claude.com/docs/en/api/messages/create), [Ollama OpenAI compatibility](https://docs.ollama.com/api/openai-compatibility), [LM Studio structured output](https://lmstudio.ai/docs/developer/openai-compat/structured-output), [Groq Llama 3.3](https://console.groq.com/docs/model/llama-3.3-70b-versatile).
