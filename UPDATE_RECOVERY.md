# AceW Admin — diagnosticarea și recuperarea după actualizări nereușite

**Stare:** ghid propus pentru revizuire; procedurile de recuperare nu au fost validate practic pe Windows.  
**Data verificării surselor:** 30 octombrie 2026.  
**Fișier propus:** `UPDATE_RECOVERY.md`, separat de `INSTALL.md` și de protocolul de testare-pilot.

## 1. Domeniu și limite

Ghidul acoperă descărcarea eșuată, instalarea întreruptă, imposibilitatea pornirii și verificarea versiunii instalate. Nu descrie un incident confirmat: nu există dovezi furnizate că actualizarea v0.1.6 a eșuat efectiv.

Acesta este un document operațional preventiv. Publicarea sa nu certifică recuperarea și nu schimbă instalatoare, versiuni sau mecanismul de actualizare. Pentru angajați, pașii care implică instalarea sau datele locale revin administratorului desemnat.

## 2. Ce știm și ce trebuie validat

| Informație | Statut și limită |
| --- | --- |
| GitHub indică v0.1.6 drept cea mai recentă versiune, publicată la 18 octombrie 2026 | Confirmat prin API-ul oficial la data verificării; verificați din nou la fiecare incident. |
| Fluxul este `App updates > Check for updates > Download update > Install & restart`; lucrul trebuie salvat înainte | Confirmat în notele oficiale v0.1.6. |
| Preferința de temă rămâne salvată pe PC | Confirmat în notele v0.1.6. |
| Instalatorul Windows x64 beta este nesemnat; protecțiile Windows nu trebuie dezactivate | Confirmat în notele v0.1.6. |
| Conturile salvate și preferințele sunt locale în profilul Windows; operațiunile de business folosesc platforma cloud comună | Context operațional furnizat pentru acest ghid; localizarea exactă, formatele și recuperarea datelor nu sunt confirmate de README sau notele versiunii verificate. |
| Repository-ul public distribuie instalatoare și metadate, fără cod sursă | Confirmat prin README; nu permite inspectarea implementării recuperării. |
| Reluarea descărcării, repararea instalării, păstrarea profilului la reinstalare, căile jurnalelor și rollback-ul | Neconfirmate. Nu presupuneți că există sau că funcționează. |

Pașii de diagnostic de mai jos sunt recomandări prudente, nu instrucțiuni oficiale AceW validate. Orice rezultat depinde de configurația concretă a PC-ului.

## 3. Înainte de intervenție

1. Salvați lucrul dacă aplicația răspunde. Notați ce operațiuni recente au fost confirmate de platformă și ce a rămas nesalvat.
2. Înregistrați ora și fusul orar, etapa eșecului, mesajul exact și versiunile cunoscute înainte și după încercare. Faceți capturi fără informații despre clienți sau autentificare.
3. Păstrați alimentarea stabilă și verificați conexiunea și spațiul liber pe unitatea sistemului și pe destinația descărcării. Nu presupuneți un necesar fix de spațiu.
4. Nu ștergeți profilul aplicației, cache-uri, foldere din AppData, fișiere de instalare ori chei de registry ca metodă de încercare. Nu folosiți programe de „curățare”.
5. Nu dezactivați Defender, SmartScreen, antivirusul sau alte protecții. Dacă apare o blocare, notați-o și cereți verificarea administratorului; nu ocoliți avertismentul.
6. Nu rulați simultan mai multe instanțe ale instalatorului și nu instalați versiuni mai vechi pentru a încerca un rollback.

## 4. Descărcarea a eșuat

**Exemple:** mesaj de eroare, fișier incomplet, progres care nu mai avansează.

1. Notați mesajul și dacă aplicația existentă încă funcționează. Lipsa progresului, singură, nu dovedește că procesul este blocat.
2. Verificați accesul normal la internet și la pagina oficială Releases, precum și spațiul liber. Dacă există o eroare de rețea sau de serviciu, încercați din nou după rezolvarea ei.
3. Dacă aplicația răspunde și descărcarea s-a încheiat explicit cu eroare, folosiți din nou `Check for updates` și `Download update`, o singură dată. Reluarea din punctul întreruperii nu este documentată; încercarea poate începe de la zero.
4. Dacă eroarea revine, opriți încercările și transmiteți diagnosticul administratorului. Dacă versiunea existentă funcționează, păstrați-o până la stabilirea intervenției.
5. Descărcarea manuală a instalatorului din pagina oficială poate fi evaluată de administrator. Existența acelui fișier nu confirmă că rularea lui repară actualizarea. Nu executați fișiere parțiale sau din surse terțe.

Nu ștergeți manual cache-ul updaterului: calea și efectul unei astfel de ștergeri nu sunt documentate.

## 5. Instalarea a fost întreruptă

**Exemple:** întrerupere de curent, repornire neprevăzută, instalator închis sau mesaj de eroare.

1. După revenirea Windows, verificați dacă există încă un instalator activ și ce mesaj afișează. Nu-l terminați forțat doar fiindcă pare lent și nu porniți altul în paralel.
2. Dacă instalarea s-a încheiat cu eroare, păstrați mesajul. Dacă Windows sau instalatorul cere explicit repornirea, salvați lucrul din celelalte aplicații și urmați solicitarea.
3. După încheierea proceselor de instalare, încercați o pornire normală a AceW Admin din scurtătura cunoscută.
4. Dacă pornește, verificați versiunea conform secțiunii 7. Faptul că pornește nu dovedește singur că actualizarea s-a finalizat.
5. Dacă pornește versiunea anterioară, consemnați rezultatul. Nu îl numiți „rollback automat”: poate fi o instalare care nu a fost aplicată.
6. Dacă nu pornește sau versiunea rămâne neclară, continuați cu secțiunea 6 și escaladați înainte de reinstalare.

Nu presupuneți că instalarea este atomică, că se repară singură ori că există un buton de reparare. Aceste comportamente necesită validare.

## 6. Aplicația nu mai pornește

1. Notați comportamentul exact: nu apare fereastra, apare și dispare, ecran gol sau mesaj Windows. Notați dacă problema a început înainte ori după `Install & restart`.
2. Verificați în Task Manager dacă AceW Admin sau instalatorul încă rulează. Nu închideți procese cu modificări posibil nesalvate și nu opriți un instalator activ fără analiza administratorului.
3. Dacă nu mai există instalare activă, salvați lucrul din celelalte aplicații și efectuați o repornire normală a Windows, apoi o singură încercare de pornire.
4. Folosiți scurtătura existentă. Administratorul poate verifica destinația ei fără a modifica fișierele; o scurtătură învechită nu dovedește coruperea aplicației.
5. Dacă apare o alertă de securitate, opriți intervenția și cereți verificarea sursei fișierului. Nu dezactivați protecțiile și nu acordați excluderi.
6. Administratorul poate consulta Reliability Monitor sau Event Viewer, dacă există evenimente relevante la ora incidentului. Absența unui eveniment nu exclude problema. Nu sunt cunoscute căi oficiale pentru jurnalele AceW; nu inventați o locație.
7. Dacă problema persistă, urmați limita de reinstalare din secțiunea 8.

Dacă există un acces web deja aprobat de companie, acesta poate fi folosit pentru verificarea datelor cloud. Confirmați mai întâi dacă ultima operațiune a fost salvată, înainte de a o reintroduce, pentru a evita dublurile.

## 7. Verificarea versiunii instalate

1. Dacă aplicația pornește, căutați versiunea afișată în interfață, inclusiv în zona `App updates`, dacă este prezentă. Locul exact al numărului versiunii nu este confirmat de documentația publică verificată.
2. Notați textul complet și comparați-l cu versiunea țintă din pagina oficială Releases. La data acestui ghid, ținta verificată este **0.1.6**.
3. Dacă aplicația nu pornește, verificați intrarea AceW Admin din lista Windows de aplicații instalate și, dacă sunt disponibile, proprietățile executabilului identificat prin scurtătură: `Properties > Details`. Acestea sunt indicii secundare și pot fi absente sau neactualizate.
4. Numele instalatorului descărcat și mesajul „up to date” nu sunt, singure, dovada versiunii care rulează.
5. Dacă informațiile diferă, consemnați toate valorile și cereți confirmarea administratorului; nu declarați actualizarea reușită.

**Criteriu de închidere:** versiunea țintă este identificată fără contradicții, aplicația se deschide normal, iar accesul autorizat la datele cloud și preferințele locale relevante sunt verificate. Nu creați operațiuni fictive în producție pentru test. Dacă lipsește o verificare, marcați incidentul „recuperare parțială” sau „neconfirmată”.

## 8. Reinstalarea — doar după evaluarea administratorului

Reinstalarea peste instalarea existentă și dezinstalarea urmată de instalare sunt intervenții diferite. Niciuna nu are aici o garanție documentată privind păstrarea conturilor salvate și a preferințelor.

- Datele locale pot fi șterse, suprascrise, migrate sau deveni incompatibile. Poate fi necesară autentificarea din nou.
- Folosirea unei platforme cloud comune nu garantează recuperarea preferințelor, sesiunilor ori lucrului nesalvat. Nu echivalați reinstalarea cu restaurarea datelor cloud.
- Înainte de orice reinstalare, administratorul trebuie să confirme locațiile exacte ale datelor pentru versiunea și utilizatorul Windows afectat, să oprească aplicația în siguranță și să facă o copie protejată, fără a modifica originalul. Nu presupuneți că o singură copie a unui folder acoperă toate datele.
- Copia poate conține tokenuri sau date de autentificare. Păstrați-o într-o locație cu acces restricționat; nu o atașați unui issue sau PR public și nu o copiați pe PC-ul altui angajat.
- Existența copiei nu garantează restaurarea: criptarea poate depinde de profilul Windows. Metoda de restaurare și compatibilitatea trebuie validate înainte de folosire.
- Dacă locațiile și metoda de protejare nu sunt confirmate, opriți-vă și cereți suportul responsabilului aplicației înainte de intervenția cu risc.
- Numai după evaluare, administratorul poate lua în calcul rularea instalatorului oficial al versiunii aprobate, fără dezinstalare prealabilă. Aceasta rămâne o procedură de testat, nu o reparare garantată.
- Dacă instalatorul solicită eliminarea datelor, schimbă neașteptat destinația sau produce un avertisment neclar, opriți intervenția și cereți clarificare.
- Dezinstalarea, resetarea profilului și restaurarea manuală a datelor nu sunt pași de rutină ai acestui ghid.

**Rollback:** nu există un mecanism confirmat în sursele verificate. Nu instalați o versiune mai veche peste date posibil migrate și nu restaurați manual executabile. Orice revenire necesită instrucțiuni explicite ale responsabilului aplicației și validarea compatibilității datelor.

## 9. Escaladare și dovezi minime

Angajatul transmite administratorului desemnat:

- PC-ul afectat printr-un identificator intern și versiunea Windows, fără parolă;
- ora incidentului și fusul orar;
- versiunea anterioară cunoscută, versiunea țintă și indiciile despre versiunea instalată;
- etapa eșecului, mesajul exact și capturi redactate;
- dacă aplicația pornește, dacă instalatorul rulează și dacă ultima operațiune cloud este confirmată;
- pașii deja efectuați și rezultatul fiecăruia.

Nu includeți parole, tokenuri, fișiere de profil sau date despre clienți în repository-ul public. Nu sunt stabilite aici un canal oficial de suport sau un termen de răspuns.

## 10. Validări necesare înainte de adoptarea pentru angajați

Aceasta este o listă de lacune de documentare, nu înlocuiește și nu modifică protocolul de testare-pilot. Responsabilul aplicației trebuie să valideze separat:

- locațiile datelor locale și ale jurnalelor, precum și identificarea versiunii;
- efectul unei descărcări eșuate și al unei reîncercări;
- comportamentul instalării întrerupte și al repornirii;
- păstrarea conturilor și preferințelor la instalarea peste versiunea existentă și la dezinstalare;
- realizarea și restaurarea unei copii locale în același profil Windows;
- eventualele migrări de date și existența unei proceduri aprobate de revenire.

Până la validare, pașii cu risc rămân exclusiv la administrator. Nu provocați întreruperi de instalare pe calculatoarele folosite pentru activitatea curentă.

## Surse și trasabilitate

1. [Release oficial v0.1.6](https://github.com/AcewProCleaning/acew-desktop-releases/releases/tag/v0.1.6) — fluxul de actualizare, salvarea lucrului, tema locală și instalatorul nesemnat.
2. [README.md oficial](https://github.com/AcewProCleaning/acew-desktop-releases/blob/main/README.md) — scopul repository-ului.
3. [GitHub API: latest release](https://api.github.com/repos/AcewProCleaning/acew-desktop-releases/releases/latest) — versiunea latest verificată la 30 octombrie 2026.
4. Contextul operațional furnizat în cererea ghidului — conturi și preferințe locale, platformă cloud comună, extinderea utilizării către angajați.

Sursele publice verificate nu oferă instrucțiuni de recuperare după eșec. Pașii suplimentari sunt propuși explicit pentru diagnostic prudent și necesită revizuire și testare practică.
