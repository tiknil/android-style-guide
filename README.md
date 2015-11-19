# android-style-guide

:exclamation: DRAFT :exclamation:

Guida di riferimento per i progetti Android in Tiknil. 
Non vuole essere l'ennesima riproposizione dello stile di stesura dei progetti in questo linguaggio, ma uno strumento utile per il team e i suoi collaboratori. 

Sentitevi liberi di dissentire da quanto abbiamo deciso di tenere come stile guida! :wink:

### References ###

*  [Android Style Google](https://source.android.com/source/code-style.html)
*  [Ribot Android Guidelines](https://github.com/ribot/android-guidelines)

### Concetti di base ###

Perché abbiamo preso certe scelte e non altre? Ecco i concetti che guidano alcune scelte esposte in questa guida (in ordine non per forza di priorità): 
* [Bellezza](https://it.wikipedia.org/wiki/Bellezza) e stile uniforme, anche nel codice
* Comprensibilità del codice da chiunque
* Velocità di scrittura del codice
* Produzione della documentazione in Italiano
* Somiglianze con altri linguaggi che utilizziamo per i progetti
* Abitudini nostre (in via di miglioramento)
* 
### Sommario ###

1. [Google Android Style Guide](#google-android-style-guide)
2. [Naming conventions](#naming-conventions)
3. [Organizzazione implementazione delle classi](#organizzazione-implementazione-delle-classi)

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

### Organizzazione implementazione delle classi ###

Forse non esiste una soluzione corretta per l'ordinamento delle parti di codice all'interno di una classe, ma utilizzarne una comune migliora la leggibilità del codice. L'ordine raccomandato è quindi: 

1. Constants
2. Fields
3. Static public methods
4. Constructors / Lifecycle
5. Custom accessors (get/set)
6. Public methods
7. Private methods
8. Override methods and callbacks (public or private)
9. Inner classes or interfaces

Si **possono** utilizzare alcuni strumenti dell'IDE Android Studio che semplificano la navigazione all'interno dei file di codice (tramite `CMD+ALT+.`) come: 

```
//region 'Region'
//endregion
```

Da utilizzare un po' come i `#pragma mark` in Obj-C nello sviluppo iOS/OSX. _Da valutare quando sono utili e quando non lo sono._

```
public class MyWonderfulObject extends ItsParentObject {
    //region Constants
    private final static String CONSTANTS = "this_constant_value";
    //endregion
   
    //region Private fields
    private String mTitle;
    private TextView mTextViewTitle;
    //endregion
    
    //region Class methods
    public static void aClassStaticMethod(){
        ...
    }
    //endregion
    
    //region Constructors / Lifecycle
    public MyWonderfulObject(){
        ...
    }
    
    @Override
    protected void onCreate(Bundle savedInstanceState){
        ...
    }
    //endregion
    
    //region Custom accessors
    public void setTitle(String title) {
        mTitle = title;
    }
    //endregion
    
    //region Public
    public void aPublicMethod(){
        ...
    }
    //endregion 
    
    //region Private
    private void setUpView() {
        ...
    }
    //endregion

    //region Override methods and callbacks
    
    // ItsParentObject
    
    @Override 
    public void methodThatHaveToBeOverriddenIntoChilds() {
        ...
    }
    //endregion
    
    //region Inner classes or interfaces
    static class AnInnerClass {

    }
    
    private class ImplementingInterfaces implements AwesomeInterface{
      ...
    }
    //endregion
} 
```

Per semplificare l'utilizzo dell'organizzazione del codice come descritto consigliamo di utilizzare il `Live template` per Android Studio apposito come descritto nel repo Android-Live Templates: basta digitare def quando si sta per stendere l'implementazione di una nuova classe.

![def_androidstudio_live_templates](http://cl.ly/image/1G2M2y1f3y0S/animation.gif)






