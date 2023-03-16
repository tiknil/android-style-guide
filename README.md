# Android Style Guide (Kotlin)

Guida di riferimento per i progetti Android in Tiknil.
Non vuole essere l'ennesima riproposizione dello stile di stesura dei progetti in questo linguaggio, ma uno strumento utile per il team e i suoi collaboratori.

Sentitevi liberi di dissentire da quanto abbiamo deciso di tenere come stile guida! :wink:

### References ###

*  [Android Style Google](https://developer.android.com/kotlin/style-guide)
*  [Jetbrains Kotlin Conding Conventions](https://kotlinlang.org/docs/coding-conventions.html)
*  [Ray Wenderlich Kotlin Style Guide](https://github.com/raywenderlich/kotlin-style-guide)

### Concetti di base ###

Perché abbiamo preso certe scelte e non altre? Ecco i concetti che guidano alcune scelte esposte in questa guida (in ordine non per forza di priorità):
* [Bellezza](https://it.wikipedia.org/wiki/Bellezza) e stile uniforme, anche nel codice
* Comprensibilità del codice da chiunque
* Velocità di scrittura del codice
* Produzione della documentazione in Italiano
* Somiglianze con altri linguaggi che utilizziamo per i progetti
* Abitudini nostre (in via di miglioramento)

### Sommario ###

1. [Google Android Style Guide](#google-android-style-guide)
2. [Naming conventions](#naming-conventions)
  - [Risorse](#risorse)
  - [Nomi dei file `layout`](#nomi-dei-file-layout)
  - [I file `values`](#i-file-values)
3. [Organizzazione implementazione delle classi](#organizzazione-implementazione-delle-classi)
4. [I file XML](#i-file-xml)
  - [Uso dei tag self-closing](#uso-dei-tag-self-closing)
  - [ID e nomi degli elementi](#id-e-nomi-degli-elementi)
  - [Nominare gli ID](#nominare-gli-id)
  - [Nominare gli ID delle stringhe](#nominare-gli-id-delle-stringhe)
  - [Ordinamento degli attributi degli elementi XML](#ordinamento-degli-attributi-degli-elementi-xml)
5. [Splashscreen](#splashscreen)
6. [Boilerplate](#boilerplate)
7. [Performances matters](#performances-matters)

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

1. I nomi delle classi vanno espressi in [UpperCamelCase](https://en.wikipedia.org/wiki/CamelCase)
2. I campi non-public (`private`, `protected`, etc) non-static e static non-final cominciano con la lettera minuscola in [lowerCamelCase](https://en.wikipedia.org/wiki/CamelCase)
3. I campi `const val` (**costanti**) sono `ALL_CAPS_WITH_UNDERSCORES` ([screaming snake case](https://kotlinlang.org/docs/coding-conventions.html#:~:text=uppercase%20underscore%2Dseparated%20(-,screaming%20snake%20case,-)%20names%3A)).

>**Nota:** non usiamo mettere `m` o `s` prima delle variabili per indicare che sono d'istanza o statiche. 

Considerare gli acronimi _come parole_ e quindi mettere solo la prima lettera maiuscola:

:+1: `XmlHttpRequest`

:-1: `XMLHTTPRequest`

#### Nomi dei metodi ####

Dichiarare i nomi del metodi in modo tale che si capisca a quale operazione servono utilizzando anche nomi dei parametri indicativi.

:+1:

```
private fun comobjOf(type: ComobjType, writable: boolean, collection: List<Comobj>): Comobj
```

:-1:

```
private fun comobjOfTypeIfWritableFromCollection(t: ComobjType, w: boolean, c: List<Comobj>): Comobj
```

> Il motivo è la miglior leggibilità e compresione da parte di un collega che deve prendere in mano il codice scritto e pensato da altri

#### Risorse ####

I nomi delle risorse (immagini, font, assets di altri tipi, xml drawable o altro) vanno scritti in **lowercase_underscore**.

#### Nomi dei file `layout` ####

I nomi dei file di `layout` dovrebbero richiaramare il nome del componente Android cui fanno riferimento, se ha senso. Guarda alla tabella seguente per degli esempi che chiariscono il concetto:

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

Come vedete non è sempre fattibile usare la convenzione espressa. E' comodo quindi considerare di nominare con il prefisso `item_` per gli oggetti che vengono utilizzati negli `Adapter` (per le `ListView`, `GridView`, etc) e dare comunque nomi che si distinuano ad componenti non standard (come espresso nell'ultima riga della colonna soprastante).

#### I file `values` ####

I file dentro la cartella `values` dovrebbero avere nome che indica il plurale: `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`

### Organizzazione implementazione delle classi ###

Forse non esiste una soluzione corretta per l'ordinamento delle parti di codice all'interno di una classe, ma utilizzarne una comune migliora la leggibilità del codice. L'ordine raccomandato è quindi:

1. Inner enums
2. Constants
3. Fields
3. Class (static) methods (`companion object { ... }` in Kotlin)
4. Constructors / Lifecycle
5. Custom accessors (get/set)
6. Public methods
7. Protected, without modifier methods
8. Private methods
9. Override methods and callbacks (public or private)
10. Inner classes or interfaces

Si **possono** utilizzare alcuni strumenti dell'IDE Android Studio che semplificano la navigazione all'interno dei file di codice (tramite `CMD+ALT+.`) come:

```
//region 'Region'
//endregion
```

```
class MyWonderfulObject: ItsParentObject {
    //region Inner enums
    //endregion

    //region Constants
    const val CONSTANT = "this_constant_value";
    //endregion

    //region Fields
    var title: String {
      get() = _title
      set() {
        _title = value
      }
    }
    
    private var _title: String;
    //endregion

    //region Class methods
    companion object {
      fun aClassStaticMethod() {
        ...
      }
    }
    //endregion

    //region Constructors / Lifecycle
    init {
        ...
    }

    @Override
    override fun onCreate(savedInstanceState: Bundle?){
        ...
    }
    //endregion

    //region Public
    fun aPublicMethod(){
        ...
    }
    //endregion

    //region Private
    private fun setUpView() {
        ...
    }
    //endregion

    //region Override methods and callbacks

    // ItsParentObject

    @Override
    override fun methodThatHaveToBeOverriddenIntoChilds() {
        ...
    }
    //endregion

    //region Inner classes or interfaces
    class AnInnerClass {

    }

    private class ImplementingInterfaces: AwesomeInterface{
      ...
    }
    //endregion
}
```

Per semplificare l'utilizzo dell'organizzazione del codice come descritto consigliamo di utilizzare il `Live template` per Android Studio apposito come descritto nel repo [AndroidStudio Live Templates](https://github.com/tiknil/AndroidStudio-Live-Templates): basta digitare `def` quando si sta per stendere l'implementazione di una nuova classe.

![def_androidstudio_live_templates](http://cl.ly/image/1G2M2y1f3y0S/animation.gif)

### I file XML ###

#### Uso dei tag self-closing ####

Quando un elemento XML non ha contenuto, deve usare un self-closing tag

:+1:

```
<TextView
    android:id="@+id/textViewProfile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

:-1:
```
<!-- Don't do this! -->
<TextView
    android:id="@+id/textViewProfile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```

#### ID e nomi degli elementi ####

Gli ID e i nomi degli elementi XML vanno espressi anch'essi in **camelCase**.

#### Nominare gli ID ####

Gli ID degli elementi XML (ovvero il campo `android:id="@+id/...` in `TextView`, `ImageView`, etc) vanno preferibilmente chiamati in questo modo:

|  prefisso  |  nome  |  suffisso  |
| --- | --- | --- |
| nome che identifica il layout in cui l'elemento è contenuto | nome che identifica a cosa serve l'elemento | suffisso con il nome che indica il tipo dell'elemento |

Per il suffisso usare le seguenti abbreviazioni:

| Elemento | Suffisso |
| -------- | -------- |
| TextView | Lbl |
| ImageView | Img |
| Button | Btn |
| EditText | Edittext |
| LinearLayout | Layout |
| RelativeLayout | Layout |

Esempi:

Un `ImageView` all'interno del file di layout dell'activity home che identifica l'icona del profilo dell'utente può essere così chiamata: `homepageProfileIconImg`

#### Nominare gli ID delle stringhe ####

 In modo similare agli ID degli elementi, per le stringhe applichiamo la seguente convenzione:

|  prefisso  |  nome  |  suffisso  |
| --- | --- | --- |
| nome che identifica la schermata o il contesto in cui l'elemento è contenuto | nome che identifica cosa deve dire la stringa | eventuale suffisso per indicare per esempio `_title` e `_message` dello stesso messaggio che si vuole dare in un `Dialog` |

#### Ordinamento degli attributi degli elementi XML ####

Usate la formattazione di Android Studio che equivale a:

1. ID
2. Style
3. Layout width e height
4. Altri attributi di layout
5. Tutto il resto

### Splashscreen ###

Compatibilmente con le specifiche del cliente/del progetto, gli splashscreen in Android sono anti-pattern. Solitamente non sono altro che una schermata con un delay per aprire la pagina successiva: la morte dello sviluppo Android.

Cerchiamo di rendere utili le splashscreen in modo da fare un buon lavoro e venire incontro alla richiesta di avere uno splashscreen come suggerito in questo [articolo di Big Nerd Ranch](https://www.bignerdranch.com/blog/splash-screens-the-right-way/)

### Boilerplate ###

Un punto di partenza per la realizzazione di progetti Android è definito nel nostro Boilerplate. Può non essere completo e le librerie vanno aggiornate, ma sicuramente permette di cominciare subito a lavorare.

[Tiknil Android Boilerplate](https://github.com/tiknil/android-boilerplate)

Leggete il readme relativo per ulteriori dettagli.

### Performances matters ###

>> Vale la pena di leggere [questo articolo di Toptal](https://www.toptal.com/android/android-performance-tips-tools) che indica a cosa fare attenzione per migliorare e debuggare le performance delle app Android

## Design pattern

### Il pattern Model-View-ViewModel

I principali attori del pattern MVVM sono:
- La _View_ he informa il ViewModel sulle azioni dell'utente e reagisce ai cambi di stato del ViewModel per la visualizzazione delle informazioni
- Il _ViewModel_  - espone flussi di dati rilevanti per la view e agisce in base agli input dell'utente per modificare i dati/avviare business logic
- Il _Model_  - astrae la fonte dei dati. Il ViewModel lavora con il DataModel per ottenere e salvare i dati.

A prima vista, il pattern MVVM sembra molto simile al modello Model-View-Presenter, perché entrambi svolgono un ottimo lavoro nell'astrazione dello stato e del comportamento della vista. Il Presentation Model astrae una View indipendente da una specifica piattaforma di interfaccia utente, mentre il pattern MVVM è stato creato per semplificare la programmazione **event driven** delle interfacce utente.

Se nel pattern MVP il Presenter indica direttamente alla View cosa visualizzare, nel MVVM **il ViewModel mostra i flussi di eventi** a cui le viste possono legarsi. In questo modo, il ViewModel non ha più bisogno di tenere un riferimento alla vista, come il Presenter fa. Ciò significa anche che tutte le interfacce che il pattern MVP richiede sono state eliminate.

Le View comunicano anche al ViewModel le diverse azioni. Pertanto, il pattern MVVM supporta l'associazione dati bidirezionale tra View e ViewModel e vi è una relazione many-to-one tra View e ViewModel. La View ha un riferimento al ViewModel ma **il ViewModel non ha informazioni sulla View**. Il consumatore dovrebbe conoscere il produttore, ma il produttore - il ViewModel - non sa, e non gli importa conoscere il consumatore.

### Model-View-ViewModel @ Tiknil

La parte event driven richiesta da MVVM viene eseguita utilizzando il functional programming, ovvero gli `Observable` di ReactiveX (Rx)
- Un riferimento all'utilizzo gli `Observable` di RxJava con il pattern MVVM è possibile trovarlo a questo link: https://medium.com/upday-devs/android-architecture-patterns-part-3-model-view-viewmodel-e7eeee76b73b


### Inversion of Control e Dependency Injection
L'*Inversion of Control* (**IoC**) è un *software design pattern* secondo il quale ogni componente dell'applicazione deve ricevere il **controllo** da un componente appartenente ad una **libreria riusabile**.<br>
L'obiettivo è quello di rendere ogni componente il più indipendente possibile dagli altri in modo che ognuno sia modificabile singolarmente con conseguente maggior riusabilità e manutenibilità.

La *Dependency Injection* (**DI**) è una forma di *IoC* dove l'implementazione del pattern avviene stabilendo le dipendenze tra un componente e l'altro tramite delle *interfacce* (chiamate **interface contracts**).<br>
A tali interfacce viene associata un'implementazione in fase di istanziazione del componente (nel *costruttore*) oppure in un secondo momento tramite *setter*.<br>
In ogni caso è generalmente presente un oggetto **container** che si occupa di creare le istanze di ogni *interfaccia*; la configurazione di tale *container* può così influenzare le dipendenze tra i vari componenti.<br>
L'utilizzo della *DI* è molto utile per la realizzazione di test automatici, infatti modificando il *container* è possibile *mockare* le dipendenze che non si desidera testare.

References:
- [Semplice video che chiarisce il concetto di DI](https://www.youtube.com/watch?v=IKD2-MAkXyQ)

### Cartelle di progetto

La cartella contenente il codice sorgente dell'app avrà la seguente struttura:

```
|-- java
  |-- com.tiknil.app
    |-- di                    # Classi per l'implementazione della dependency injection con Dragger2
    |-- utils                 # Classi di generico aiuto per il modulo app
    |-- views                 # Le classi che implementano la ui
        |-- activities        # Implemetazione delle activity eventualmente inseriti in sottocartelle di sezione
        |-- fragments         # Implementazione dei fragment eventualmente inseriti in sottocartelle di sezione
    |-- viewmodels            # Tutti i viewmodel eventualmente inseriti in sottocartelle di sezione
    |-- assets
      |-- fonts               # Contiene i file dei fonts
    |-- res                   # Cartella di resources: color, drawable, layout,...
  |-- com.tiknil.app.core
    |-- services              # Interfacce per l'implementazione dei servizi
    |-- views                 # Classi base per l'implementazione delle view Activity e Fragment
    |-- viewmodels            # Classi base per l'implementazione dei viewModel
    |-- (models)              # Le classi dei modelli se non si crea un modulo apposta, dipende dal progetto
  |-- com.tiknil.app.services # Implementazione dei services (providers) come networking, persistenza dei dati,
  |-- com.tiknil.app.models   # Tutti gli oggetti model

```

Si veda il progetto boilerplate (kotlin-boilerplate-mvvm)[https://github.com/tiknil/kotlin-boilerplate-mvvm/blob/master/README.md] per maggiori dettagli
