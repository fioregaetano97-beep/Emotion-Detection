# EmotionDetection — Applicazione di rilevamento delle emozioni con Watson NLP

Applicazione web Flask che rileva le emozioni (rabbia, disgusto, paura, gioia,
tristezza) espresse in un testo, tramite il servizio Watson NLP Runtime.

## Struttura

```
.
├── EmotionDetection/
│   ├── __init__.py            # importa emotion_detector (Attività 4)
│   └── emotion_detection.py   # logica + gestione errori (Attività 2, 3, 7)
├── templates/index.html
├── static/mywebscript.js
├── server.py                  # deployment Flask (Attività 6, 7)
└── test_emotion_detection.py  # test unitari (Attività 5)
```

---

## Attività 1 — Pubblicare su GitHub

Questo README (nome progetto: **EmotionDetection**) va incluso nel repository
pubblico. Comandi per pubblicarlo dal tuo account:

```bash
git init
git add .
git commit -m "Emotion Detection app with Watson NLP"
git branch -M main
git remote add origin https://github.com/<tuo-utente>/EmotionDetection.git
git push -u origin main
```

Invia l'URL: `https://github.com/<tuo-utente>/EmotionDetection`

## Attività 2 — Applicazione di rilevamento emozioni

Vedi `EmotionDetection/emotion_detection.py`, funzione `emotion_detector`.

**Output terminale (import + test senza errori):**
```
>>> Test import ed esecuzione del pacchetto EmotionDetection
Risultato: {'anger': 0.01, 'disgust': 0.01, 'fear': 0.01, 'joy': 0.95, 'sadness': 0.01, 'dominant_emotion': 'joy'}
```

> Nota: l'endpoint Watson NLP (`sn-watson-emotion.labs.skills.network`) è
> raggiungibile solo da un ambiente IBM Skills Network Labs. Nel tuo ambiente
> di laboratorio la chiamata sarà reale; qui è stata simulata per validare
> la logica dell'applicazione.

## Attività 3 — Formattazione dell'output

Il formato richiesto viene prodotto in `server.py`:
```
For the given statement, the system response is 'anger': 0.02, 'disgust': 0.02,
'fear': 0.02, 'joy': 0.9 and 'sadness': 0.02. The dominant emotion is joy.
```

## Attività 4 — Validazione del pacchetto

`EmotionDetection/__init__.py` contiene:
```python
from EmotionDetection.emotion_detection import emotion_detector
```

**Output terminale di validazione:**
```bash
$ python3 -c "from EmotionDetection import emotion_detector; print(emotion_detector('I am glad this happened'))"
{'anger': 0.01, 'disgust': 0.01, 'fear': 0.01, 'joy': 0.95, 'sadness': 0.01, 'dominant_emotion': 'joy'}
```
Nessun errore di import → il pacchetto è valido.

## Attività 5 — Test unitari

```bash
python3 -m unittest test_emotion_detection -v
```

**Output ottenuto:**
```
test_blank_input ... ok
test_emotion_detector ... ok

----------------------------------------------------------------------
Ran 2 tests in 0.002s

OK
```

## Attività 6 — Distribuzione Flask

```bash
python3 server.py
```

Apri il browser su `http://localhost:5000`, inserisci un testo e premi
"Analizza". **Cattura lo screenshot come `6b_deployment_test.png`.**

## Attività 7 — Gestione degli errori

- `emotion_detection.py`: se il servizio risponde con status 400 (o l'input è
  vuoto), la funzione restituisce tutti i valori a `None`.
- `server.py`: se `textToAnalyze` è vuoto o il risultato ha `dominant_emotion`
  `None`, l'app risponde `"Invalid text! Please try again!"` con status 400.

Per lo screenshot `7c_error_handling_interface.png`: sulla pagina web invia
il modulo lasciando il campo testo vuoto (o prova l'URL
`/emotionDetector?textToAnalyze=` direttamente) e cattura la risposta
"Invalid text! Please try again!".

## Attività 8 — Analisi statica

```bash
pip install --break-system-packages pylint
pylint server.py
```

**Output ottenuto:**
```
Your code has been rated at 10.00/10
```
