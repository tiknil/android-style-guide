# android-style-guide

:exclamation: DRAFT :exclamation:

Guida di riferimento per i progetti Android in Tiknil. 
Non vuole essere l'ennesima riproposizione dello stile di stesura dei progetti in questo linguaggio, ma uno strumento utile per il team e i suoi collaboratori. 

Sentitevi liberi di dissentire da quanto abbiamo deciso di tenere come stile guida! :wink:

### References ###

*  [Android Style Google](https://source.android.com/source/code-style.html)
*  [Ribot Android Guidelines](https://github.com/ribot/android-guidelines)

### Sommario ###

1. [Google Android Style Guide](#Google-Android-Style-Guide)
2. [Naming conventions](#naming-conventions)


### Google Android Style Guide ###

Per quanto riguarda i seguenti argomenti aderiamo completamente alla [Android Style Google](https://source.android.com/source/code-style.html) by Google: 

1. **Exceptions**
2. **Javadoc comments**
3. **Variables scope**
4. **Ordine degli `import`** (ci pensa Android Studio)
5. **Indentazione** (ci pensa Android Studio)
6. **Naming conventions**, riproposte nell'apposito capitolo per chiarezza ed evidenza: [Naming conventions](#naming-conventions)
7. **Brace style**
8. Uso di **Standard Java Annotations**
9. commenti **`//TODO:`**
10. **BE CONSISTENT** concept

### Naming conventions ###

1. I campi non-public (`private`, `protected`, etc) non-static cominciano per `m`.
2. I campi statici non-final cominciano con la lettare `s`.
3. I campi `static` `final` (**costanti**) sono `ALL_CAPS_WITH_UNDERSCORES`.
4. Tutti gli altri campi cominciano con la lettera minuscola.

Considerare gli acronimi _come parole_ e quindi mettere solo la prima lettera maiuscola: 

:+1: `XmlHttpRequest`

:-1: `XMLHTTPRequest`


