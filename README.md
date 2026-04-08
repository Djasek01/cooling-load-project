# Cooling Load Prediction Project

## 1. Uvod

U suvremenom energetskom planiranju zgrada važno je što ranije procijeniti buduću potrebu za hlađenjem prostora. Takva procjena omogućuje pravilno postavljanje rashladnih uređaja, optimizaciju potrošnje energije i smanjenje troškova investicije i eksploatacije. Ručni termotehnički proračuni često su vremenski zahtjevni, a ovise o velikom broju ulaznih parametara.

Cilj ovog projekta je istražiti mogućnosti primjene metoda otkrivanja znanja u podacima za predviđanje toplinskog učinka hlađenja zgrada na temelju dostupnog skupa podataka. Projekt je strukturiran po fazama CRISP‑DM metodologije: razumijevanje domene, razumijevanje podataka, priprema podataka, modeliranje, vrednovanje i korištenje rezultata.

## 2. Razumijevanje domene

### 2.1. Poslovni ciljevi i ciljevi rudarenja podataka

Promatrani poslovni problem odnosi se na izbor odgovarajuće snage rashladnog uređaja za stambeni objekt. Pretpostavljeni klijent može biti proizvođač ili prodavač rashladnih uređaja, projektantski ured ili energetski savjetnik koji želi brzo procijeniti potrebni cooling load na temelju osnovnih informacija o zgradi.

Primarni poslovni cilj je omogućiti brzu i dovoljno točnu procjenu potrebnog toplinskog učinka hlađenja bez provođenja detaljnog energetskog proračuna za svaki pojedini objekt. Dodatni ciljevi uključuju bolje razumijevanje utjecaja pojedinih građevinskih značajki (npr. kompaktnosti, površine ostakljenja, orijentacije) na potrebu za hlađenjem te identifikaciju tipova zgrada s najvećim zahtjevima.

Cilj rudarenja podataka je izgraditi regresijski model koji na temelju ulaznih značajki zgrade predviđa kontinuiranu vrijednost cooling load‑a. Uspješnost rješenja mjeri se pomoću standardnih regresijskih metrika (npr. RMSE, MAE, R²), pri čemu je poželjno da odstupanje procjene ne dovodi do odabira značajno preslabog ili predimenzioniranog rashladnog uređaja.

### 2.2. Analiza troškova i koristi

Troškovi ovakvog projekta uključuju prikupljanje i pripremu podataka o zgradama, vrijeme potrebno za razvoj i evaluaciju modela te kasnije održavanje rješenja. U stvarnom poslovnom okruženju to znači angažman stručnjaka za energetiku, podatkovne znanstvenike i informatičare, kao i računalne resurse za pohranu i obradu podataka.

Potencijalne koristi su višestruke: skraćuje se vrijeme izrade ponuda i tehničkih rješenja za kupce, smanjuje se rizik od pogrešnog dimenzioniranja opreme, a samim time i trošak ulaganja te potrošnje energije. Dodatno, model se može koristiti kao alat u prodajnom procesu, gdje prodavač unosom nekoliko osnovnih parametara zgrade dobiva preporučeni raspon snaga uređaja. Ako se model koristi na većem broju projekata kroz dulje razdoblje, očekuje se da ukupne koristi nadmašuju početne troškove razvoja.

### 2.3. Pregled literature

- koje podatke autori koriste (geometrija zgrade, materijali, klima, način korištenja prostora)
- koje metode modeliranja primjenjuju (npr. višestruka linearna regresija, umjetne neuronske mreže, SVM, ansambl metode)
- koje metrike koriste za evaluaciju te kakvu razinu točnosti postižu
- u kojoj je mjeri pristup primjenjiv u praksi


## 3. Razumijevanje podataka

### 3.1. Opisivanje podataka

Skup podataka `cooling_load.csv` sastoji se od 768 instanci i 9 atributa, pri čemu 8 atributa predstavlja ulazne značajke, a jedan atribut je ciljna varijabla *Cooling Load*. Svi atributi su numerički, bez nedostajućih vrijednosti.

Ulazne značajke su: 

- **Relative Compactness** – relativna kompaktnost tlocrta zgrade.  
- **Surface Area** – ukupna površina ovojnice zgrade.  
- **Wall Area** – površina zidova.  
- **Roof Area** – površina krova.  
- **Overall Height** – ukupna visina zgrade.  
- **Orientation** – kodirana orijentacija zgrade.  
- **Glazing Area** – udio ostakljene površine.  
- **Glazing Area Distribution** – raspodjela ostakljenja po fasadama.  

Ciljna varijabla *Cooling Load* izražava toplinski učinak hlađenja koji je potrebno osigurati za promatranu zgradu.

### 3.2. Istraživanje podataka

Za svaki atribut izračunate su osnovne deskriptivne statistike (minimum, maksimum, srednja vrijednost, standardna devijacija i kvartili), te će se u notebookima izraditi grafički prikazi poput histograma i box‑plotova.

Primijećeno je da se atribut **Overall Height** javlja u dvjema razinama (npr. prizemnica i katnica), dok **Glazing Area** uzima nekoliko diskretnih vrijednosti koje predstavljaju različite razine ostakljenja. Distribucija ciljne varijable **Cooling Load** pokazuje raspon približno od 10.9 do 48.03, sa srednjom vrijednosti oko 24.6 jedinica. Dodatno će se analizirati korelacije između značajki, posebice utjecaj površine i ostakljenja na potrebni cooling load. 

### 3.3. Provjera kvalitete podataka

Skup podataka je potpun: nijedan atribut ne sadrži nedostajuće vrijednosti, a broj instanci je jednak u svim stupcima. Nisu uočene posebne šifre za nedostajuće ili nepoznate vrijednosti (poput −1, 999 i sl.), niti postoje prazna polja.

Rasponi vrijednosti pojedinih značajki su realni i konzistentni s opisom problema (geometrija jednostavnih stambenih zgrada). Potencijalni outlieri provjeravaju se grafički i statistički, ali se zbog sintetičke prirode skupa podataka pretpostavlja da su sve kombinacije atributa namjerne i mogu ostati u daljnjoj analizi.

## 4. Struktura repozitorija

```text
cooling-load-project/
├── data/
│   ├── raw/
│   │   └── cooling_load.csv
│   └── processed/
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_preparation.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_evaluation.ipynb
├── reports/
│   ├── figures/
│   └── literature/
├── src/
│   ├── data_preprocessing.py
│   ├── train_model.py
│   └── evaluate_model.py
├── .gitignore
└── README.md
```

## 5. Tehnologije

- Python  
- pandas, numpy  
- matplotlib / seaborn  
- scikit‑learn  
- Jupyter Notebook  
