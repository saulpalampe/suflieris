# Lugas sagatavošana Suflierim ar AI palīdzību

[← Atpakaļ uz projekta aprakstu](README.md) · [Pilnā instrukcija](INSTRUKCIJA.md)

Šī ir īsa pamācība tiem, kas Suflieri izmēģina pirmo reizi. Rezultātā būs divi faili: **audio fails** un **SRT fails** Suflierim saprotamā formā.

**Pirmajai reizei izmēģiniet vienu ainu (5–10 minūtes teksta)**, nevis visu lugu. Tā ātri redzēsiet visu ceļu un kļūdas izlabosiet ar mazu darbu.

## Īsumā

| Solis | Ko dara | Rīks |
| --- | --- | --- |
| 1 | Aktieri nolasa tekstu, to ieraksta | Diktofons, telefons vai mikrofons |
| 2 | Izgriež kļūdas un garās pauzes, pievieno skaņas beigās | Audacity |
| 3 | Runas atpazīšana ar laikiem → SRT | Subtitle Edit (Whisper) |
| 4 | Faila beigās iezīmē skaņas | Subtitle Edit |
| 5 | SRT + lugas teksts → Suflieris formāts | AI modelis ar zemāk doto uzdevumu |
| 6 | Pārbauda un pielabo | Subtitle Edit un Suflieris |

**Vissvarīgākais noteikums:** kad SRT ir izveidots (3. solis), **audio failu vairs nedrīkst mainīt**. Katra izgriezta vai pievienota sekunde nobīda visus turpmākos laikus. Tāpēc vispirms pabeidziet audio, tikai tad veidojiet subtitrus.

## 1. Ierakstiet tekstu

- Aktieri lasa savas replikas pēc kārtas. **Lomu vārdus, remarkas un nodaļu nosaukumus nelasa.**
- Starp replikām atstājiet pauzi **apmēram 1 sekundi**.
- Kļūdas gadījumā pasakiet frāzi vēlreiz no sākuma. Lieko izgriezīs 2. solī.
- Klusa telpa, mikrofons vienā attālumā no visiem. Telefona diktofons pietiek.

## 2. Apstrādājiet audio (Audacity)

1. Izgrieziet kļūdas, atkārtojumus un troksni.
2. Garās pauzes saīsiniet, bet **starp replikām atstājiet 0,5–1 s**. Automātiski to dara *Effect → Truncate Silence* (piemēram, saīsināt pauzes, kas garākas par 1 s, līdz 0,8 s).
3. Izlīdziniet skaļumu: *Effect → Loudness Normalization* (–16 LUFS), lai visi aktieri skan vienādi skaļi.
4. **Skaņas efektus un mūziku pievienojiet faila beigās**, aiz pēdējās replikas, pa vienam, ar ~2 s pauzi starp tiem. Pierakstiet to secību un īsu nosaukumu, piemēram, „Durvju klauvējiens”.
5. Eksportējiet: *File → Export → MP3*, 128–192 kbps.

## 3. Iegūstiet SRT ar laikiem

**Ieteicamais variants: Subtitle Edit ar Whisper** (bezmaksas, darbojas datorā bez interneta, saprot latviešu valodu).

1. Atveriet MP3 Subtitle Edit: *Video → Open video file*.
2. *Video → Audio to text (Whisper)*, valoda **Latvian**, modelis pēc iespējas lielāks (piemēram, *large*). Pirmajā reizē programma modeli lejupielādēs.
3. Kad apstrāde beigusies, saglabājiet: *File → Save as*, formāts *SubRip (.srt)*, kodējums UTF-8.

Der arī jebkurš cits runas atpazīšanas rīks vai pakalpojums, kas prot eksportēt **SRT ar laikiem**. Galvenais, lai tas apstrādā **tieši to pašu MP3 failu**, ko lietosiet Suflierī.

## 4. Iezīmējiet skaņas faila beigās (Subtitle Edit)

Runas atpazīšana skaņas neatpazīst, bet AI modelis nedzird audio. Tāpēc skaņu vietas iezīmē cilvēks.

1. Subtitle Edit viļņa attēlā aizejiet līdz faila beigām, kur ir skaņas.
2. Izdzēsiet blokus, ko Whisper tur izdomājis (bieži tur ir neesošs teksts).
3. Katrai skaņai iezīmējiet bloku no sākuma līdz beigām un ierakstiet:
   - `SKAŅA: Durvju klauvējiens` – īsai skaņai;
   - `FONS: Vējš stacijā` – fona skaņai vai mūzikai.
4. Saglabājiet SRT.

Skaņu nosaukumi lai ir īsi un saprotami. AI modelis tos pārkopēs uz vietām lugas tekstā.

## 5. Apvienojiet ar lugas tekstu (AI modelis)

Jums vajag:
- SRT no 4. soļa;
- lugas tekstu elektroniski (Word, PDF vai teksts) ar lomu vārdiem, cēlieniem, ainām un remarkām par skaņām.

Atveriet AI modeli (piemēram, Claude, ChatGPT vai Gemini). Iekopējiet zemāk esošo uzdevumu un pievienojiet abus failus vai iekopējiet to saturu attiecīgajās vietās. Saglabājiet atbildē doto SRT kā teksta failu ar paplašinājumu `.srt` un kodējumu UTF-8.

**Garai lugai** apstrādājiet pa cēlieniem: sadaliet SRT un lugas tekstu pa cēlieniem, katru dodiet atsevišķi un rezultātus salieciet secīgi vienā failā. Skaņu blokus faila beigās pievienojiet tikai vienreiz, pēdējā daļā. Pārāk garu tekstu modelis var apstrādāt nepilnīgi vai saīsināt.

### Uzdevums AI modelim

````text
Tu palīdzi sagatavot subtitru (SRT) failu programmai "Suflieris", kas teātra izrādē atskaņo aktieriem replikas no viena audio ieraksta.

Tev ir divi ievaddati:
1. SRT_FAILS – automātiski atpazīts lugas ieraksts. Laiki ir precīzi, bet teksts var saturēt kļūdas, un bloku robežas ne vienmēr sakrīt ar replikām. Faila beigās, aiz pēdējās replikas, cilvēks jau iezīmējis skaņu blokus ar `SKAŅA:` vai `FONS:`.
2. LUGAS_TEKSTS – oriģinālais lugas teksts ar lomu vārdiem, cēlieniem, ainām un remarkām.

UZDEVUMS: izveido vienu SRT failu Suflieris formātā, kurā SRT_FAILS laiki ir apvienoti ar LUGAS_TEKSTS saturu.

SUFLIERIS FORMĀTS
Katrs bloks: kārtas numurs, laika rinda `HH:MM:SS,mmm --> HH:MM:SS,mmm`, teksts, tukša rinda. Bloku veidi pēc teksta sākuma:
- Replika: `VĀRDS: teksts`. Lomas vārds AR LIELAJIEM BURTIEM, vienādi visā failā, kā tas ir lugas tekstā (piemēram `MARTA:`). Kopīga replika: `MARTA, ERNESTS: teksts`.
- Replikas turpinājums: ja vienas lomas replika sadalīta vairākos blokos, lomas vārdu raksti tikai pirmajā blokā, nākamajos tikai tekstu.
- Remarka: viss bloka teksts iekavās, piemēram `(Marta iziet.)`. Iekļauj tikai īsas remarkas, kas palīdz sekot darbībai.
- Virsraksts: `# Cēliena nosaukums`, `## Ainas nosaukums`, `### Skata nosaukums` – tā, kā tos nosaucis autors.
- Skaņa tekstā: `SKAŅA: nosaukums` (īsa skaņa) vai `FONS: nosaukums` (fona skaņa vai mūzika). Fonam, kam jāskan bez pārtraukuma līdz apturēšanai, pievieno ` (cilpa)`.

NOTEIKUMI
1. LAIKI. Replikām izmanto tikai SRT_FAILS esošos laikus. Laikus neizdomā un nemaini.
   - Ja vienai replikai atbilst vairāki SRT bloki, apvieno tos: sākums no pirmā bloka, beigas no pēdējā. Ja replika ir ļoti gara (vairāk nekā ~20 sekundes), vari atstāt to vairākos blokos kā turpinājumus.
   - Ja vienā SRT blokā ir divu lomu replikas, sadali to divos blokos, sadalot laiku proporcionāli teksta garumam. Šādu vietu iekļauj pārskatā kā pārbaudāmu.
2. TEKSTS. Replikas tekstu ņem no LUGAS_TEKSTS, nevis no atpazītā teksta. Ja ierakstā aktieris teicis citādi nekā lugā (izlaists vai pievienots teikums), seko ierakstam un iekļauj to pārskatā.
3. NEIERAKSTĪTAIS. Ja kāda lugas replika ierakstā nav nolasīta, to neiekļauj kā repliku, bet min pārskatā. Ja SRT_FAILS ir teksts, kura nav lugā (atkārtojums, kļūda), to neiekļauj un min pārskatā.
4. VIRSRAKSTI, REMARKAS UN SKAŅAS TEKSTĀ nav ierakstā, tāpēc tiem dod īsu laiku pauzē starp blakus esošajiem blokiem: tam jāsākas pēc iepriekšējā bloka beigām un jābeidzas pirms nākamā bloka sākuma, ilgums 0,02–0,30 s. Bloki nedrīkst pārklāties, un beigu laikam jābūt lielākam par sākuma laiku. Ja vairāki šādi bloki ir vienā pauzē, sadali to starp tiem.
5. SKAŅAS. Kur LUGAS_TEKSTS remarkās minēta skaņa, kurai SRT_FAILS beigās ir atbilstošs skaņu bloks, ievieto tajā vietā tekstā bloku ar TIEŠI TĀDU PAŠU nosaukumu un veidu (`SKAŅA:` vai `FONS:`) kā beigās. Skaņu blokus SRT_FAILS beigās atstāj nemainītus un faila beigās. Ja skaņa minēta lugā, bet beigās tai nav bloka, vai otrādi, min to pārskatā.
6. SECĪBA. Bloki seko lugas secībai. Numurē blokus no 1 pēc kārtas.
7. Nekādu HTML vai citu formatējumu tekstā.

ATBILDES FORMĀTS
1. Viss gatavais SRT vienā koda blokā, nekas netiek izlaists vai saīsināts.
2. Pēc tam īss pārskats: numurēts saraksts ar vietām, kas cilvēkam jāpārbauda Subtitle Edit (bloka numurs un iemesls). Ja nekas nav jāpārbauda, raksti "Pārbaudāmu vietu nav".

PIEMĒRS (saīsināts)
SRT_FAILS fragments:
1
00:00:00,607 --> 00:00:03,007
vilciens kavējas jau trešo stundu vai tas vispār pienāks

2
00:00:03,400 --> 00:00:07,900
pienāks vilcieni vienmēr pienāk tikai ne tad kad mēs gaidām

3
00:01:55,989 --> 00:01:59,529
SKAŅA: Tāla vilciena svilpe

LUGAS_TEKSTS fragments:
1. CĒLIENS
1. aina. Stacija vakarā
Maza stacija. Vakars. Marta sēž uz čemodāna.
MARTA. Vilciens kavējas jau trešo stundu. Vai tas vispār pienāks?
Tālumā svilpe.
ERNESTS. Pienāks. Vilcieni vienmēr pienāk, tikai ne tad, kad mēs gaidām.

Rezultāts:
1
00:00:00,000 --> 00:00:00,200
# 1. CĒLIENS

2
00:00:00,200 --> 00:00:00,350
## 1. aina. Stacija vakarā

3
00:00:00,350 --> 00:00:00,550
(Maza stacija. Vakars. Marta sēž uz čemodāna.)

4
00:00:00,607 --> 00:00:03,007
MARTA: Vilciens kavējas jau trešo stundu. Vai tas vispār pienāks?

5
00:00:03,100 --> 00:00:03,300
SKAŅA: Tāla vilciena svilpe

6
00:00:03,400 --> 00:00:07,900
ERNESTS: Pienāks. Vilcieni vienmēr pienāk, tikai ne tad, kad mēs gaidām.

7
00:01:55,989 --> 00:01:59,529
SKAŅA: Tāla vilciena svilpe

SRT_FAILS:
[iekopē šeit]

LUGAS_TEKSTS:
[iekopē šeit]
````

## 6. Pārbaudiet

**Subtitle Edit**

1. Atveriet jauno SRT kopā ar to pašu MP3.
2. Izejiet cauri vietām, ko AI minējis pārskatā. Viļņa attēlā pārbaudiet, vai blokā ir tieši viena replika un vai robežas nenogriež zilbes.
3. Ja Subtitle Edit brīdina par pārklājumiem vai nesakārtotiem laikiem skaņu blokos faila beigās, tas ir normāli.
4. Saglabājiet kā UTF-8.

**Suflieris**

1. Ielādējiet MP3 un SRT.
2. Pārbaudiet paziņojumu augšā, piemēram, *„58 replikas, 6 lomas, 9 skaņas (9 no skaņu bloka faila beigās), 4 virsraksti”*:
   - lomu skaits sakrīt ar lugu (lieka loma nozīmē atšķirīgi uzrakstītu vārdu);
   - visas skaņas ir „no skaņu bloka faila beigās” (ja nav, nosaukumi tekstā un beigās nesakrīt).
3. Stabiņā **Saturs** jābūt visiem cēlieniem un ainām.
4. Noklausieties dažas replikas sākumā, vidū un beigās. Ja visas sākas par agru vai par vēlu, lietojiet **Laika nobīdi**. Ja tiek nogrieztas zilbes, palieliniet **Rezervi** iestatījumos.

## Biežākās kļūdas

| Kas notiek | Iemesls | Ko darīt |
| --- | --- | --- |
| Laiki nesakrīt nekur | Audio mainīts pēc SRT izveides | Atkārtojiet 3. soli ar galīgo audio |
| Laiki nobīdās no kādas vietas | AI izlaidis vai sajaucis blokus | Salīdziniet to vietu ar SRT no 3. soļa |
| Lomu ir vairāk nekā lugā | Vārds uzrakstīts dažādi | Izlabojiet vārdu SRT failā |
| Skaņa neskan vai skan nepareiza | Nosaukums tekstā un beigās atšķiras | Izlabojiet nosaukumu, lai tie sakristu |
| AI atbilde beidzas pusē | Teksts pārāk garš | Apstrādājiet pa cēlieniem |
