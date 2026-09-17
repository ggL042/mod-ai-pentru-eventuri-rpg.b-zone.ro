<div align="center">

# 🤖 B-Zone Event AI

### AI automat pentru eventurile de pe RPG.B-Zone.ro

![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?logo=windows)
![SA-MP](https://img.shields.io/badge/SA--MP-B--Zone-orange)
![MoonLoader](https://img.shields.io/badge/MoonLoader-Lua-blueviolet)
![AI](https://img.shields.io/badge/AI-Groq-success)

</div>

---

## 📦 1. Instalare rapidă

### ⭐ MP complet cu modul deja instalat

Cea mai simplă variantă este să descarci direct MP-ul complet, cu modul și toate dependențele deja integrate:

### 👉 [Descarcă Freddie SAMP + B-Zone Event AI](https://drive.google.com/file/d/1t7wgi5iUDtNtg7M2PwYh--qPBcIwAstZ/view?usp=sharing)

Extrage arhiva și pornește jocul.

> Dacă folosești varianta completă, nu mai trebuie să instalezi manual MoonLoader, SAMP.Lua sau cURL.

---

## 🛠️ 2. Instalare manuală

Dacă ai deja propriul GTA San Andreas / SA-MP, ai nevoie de următoarele:

| Componentă        | Download                            |
| ----------------- | ----------------------------------- |
| 🎮 SA-MP / B-Zone | https://www.b-zone.ro/samp          |
| 🌙 MoonLoader     | https://www.blast.hk/moonloader/    |
| ⚙️ SAMPFUNCS      | https://www.blast.hk/threads/17/    |
| 📚 SAMP.Lua       | https://github.com/THE-FYP/SAMP.Lua |
| 🌐 cURL Windows   | https://curl.se/windows/            |
| 🤖 Groq API Key   | https://console.groq.com/keys       |

---

## 📂 3. Instalarea modului

Copiază:

```text
BZoneEventAI.lua
```

în:

```text
GTA San Andreas\moonloader\
```

---

## 📚 4. Instalarea SAMP.Lua

Descarcă **SAMP.Lua** și copiază folderul:

```text
samp
```

în:

```text
GTA San Andreas\moonloader\lib\
```

Trebuie să existe:

```text
GTA San Andreas\moonloader\lib\samp\events.lua
```

---

## 🌐 5. Instalarea cURL

Pe Windows 10 / 11, `curl.exe` există de obicei deja în sistem.

Pentru ca modul să aibă propriul cURL și să nu depindă de instalarea Windows, descarcă versiunea **Windows x64**:

### 👉 https://curl.se/windows/

Din arhivă copiază:

```text
curl.exe
curl-ca-bundle.crt
```

în:

```text
GTA San Andreas\moonloader\lib\
```

Structura finală ar trebui să fie:

```text
GTA San Andreas\
│
└── moonloader\
    │
    ├── BZoneEventAI.lua
    │
    └── lib\
        │
        ├── curl.exe
        ├── curl-ca-bundle.crt
        │
        └── samp\
            └── events.lua
```

> `curl.exe` nu trebuie adăugat manual în PATH.

---

## 🎮 6. Comenzile modului

| Comandă     | Ce face                                          |
| ----------- | ------------------------------------------------ |
| `/aievents` | ✅ Pornește sau oprește automatizarea eventurilor |
| `/aistatus` | 📊 Arată stat                                    |
