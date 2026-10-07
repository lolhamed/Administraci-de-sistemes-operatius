
## SPRINT 1


JO faré un keylogger:



Primer, he instal·lat,l'entorn d'escriptori XFCE, l'eina de captures scrot, Python i Flask. Durant la configuració dels paquets apareix la selecció del gestor d'inici de sessió i es tria LightDM.



<img width="636" height="464" alt="image" src="https://github.com/user-attachments/assets/fa4d53e9-2e2e-40a6-85d5-1f05630645c8" />

___


EScollim lightdm
<img width="628" height="472" alt="image" src="https://github.com/user-attachments/assets/36f783f4-ac5f-4b68-ab47-ffb260a82606" />


____


Comprovem que esta tot instal·lat:
<img width="485" height="73" alt="image" src="https://github.com/user-attachments/assets/67833255-4d3c-40a4-9552-27d0bf592428" />




Instal·lem el compilador i les eines per poder configurar el nostre futur keylogger:

<img width="638" height="416" alt="image" src="https://github.com/user-attachments/assets/70a1d3ca-3200-4a4c-9535-890d9dee260f" />


Clonem el repositori de logkeys i podem veure que s'ha descarregat:

<img width="631" height="170" alt="image" src="https://github.com/user-attachments/assets/99d99a90-e3aa-44bd-ac4f-f568f38075ec" />



Aquest script genera els fitxers necessaris per poder executar i iniciar la configuració:
<img width="479" height="222" alt="image" src="https://github.com/user-attachments/assets/4ec1facd-8ff3-421d-960c-884e2f7bef7d" />


Configurem la compilació desde el directori build:
<img width="575" height="388" alt="image" src="https://github.com/user-attachments/assets/1beba456-80c0-4e7b-835d-34b02507ef16" />

Ara compilem el logkeys:
<img width="1206" height="667" alt="image" src="https://github.com/user-attachments/assets/12c29a01-5c9b-4c35-97bb-134cb1ce8ffd" />

Instal·lem el programa:
<img width="888" height="716" alt="image" src="https://github.com/user-attachments/assets/b2614d25-b942-492f-9960-a68657e6aaf6" />


Mirem la versió:
<img width="808" height="492" alt="image" src="https://github.com/user-attachments/assets/a24a53ca-733d-4c4b-bb54-ca2ca42af898" />


<img width="940" height="591" alt="image" src="https://github.com/user-attachments/assets/5c1254b4-ff59-4d1d-907d-0e1c3139e8ef" />

Comanda: localectl status | grep -i keymap

Consulta el mapa de teclat de consola. La sortida indica que VC Keymap no està definit, motiu pel qual les proves passen explícitament un mapa a logkeys


Comanda: localectl status

Mostra la configuració regional i del teclat: VC Keymap: (unset) i X11 Layout: es. Això confirma que el teclat gràfic és espanyol, mentre que el mapa de consola no està definit.

<img width="543" height="154" alt="image" src="https://github.com/user-attachments/assets/b11d9757-f1eb-40a7-82d7-534809f4f5f4" />


El fitxer s'ha escrit correctament al directori comu (ubuntu.map)
<img width="884" height="93" alt="image" src="https://github.com/user-attachments/assets/0827cfa5-dd05-43c4-836d-46da4a466e30" />

LListem els mapes instal·lats:
<img width="689" height="563" alt="image" src="https://github.com/user-attachments/assets/aeb62dd0-81d1-4d59-8f8f-c3c76d5b5f89" />

Després s'escriu una frase al terminal com si fos una comanda i el shell respon que hola no s'ha trobat; a més, el fitxer no es pot llegir sense privilegis (cat: /tmp/test.log: Permission denied). Amb sudo cat /tmp/test.log es pot comprovar que hi ha registres, però la descodificació no és correcta.

<img width="1204" height="187" alt="image" src="https://github.com/user-attachments/assets/6fd9ab10-b794-4876-b5c8-438dedc542c5" />


Comandes: head -5 /usr/local/share/logkeys/keymaps/lluc.map i sudo pkill -f logkeys

Inspecciona les primeres línies del mapa personalitzat i atura la instància de prova abans de repetir-la amb un altre mapa.

<img width="757" height="138" alt="image" src="https://github.com/user-attachments/assets/6b60888a-25fc-4a45-a5d2-1c72b7ef072d" />

<img width="500" height="41" alt="image" src="https://github.com/user-attachments/assets/f978e03d-d264-4373-baec-a3d658fb55d4" />



Comanda: sudo logkeys --start --output /tmp/test_es.log --keymap /usr/local/share/logkeys/keymaps/es_ES.map

Inicia una nova prova utilitzant el mapa espanyol es_ES.map, en lloc del mapa personalitzat anterior.
<img width="1055" height="46" alt="image" src="https://github.com/user-attachments/assets/959dc965-9288-4a6f-8812-23b417ac48d3" />


<img width="510" height="170" alt="image" src="https://github.com/user-attachments/assets/527348a7-dbbf-48ab-a48a-7ac53c184f31" />


<img width="814" height="77" alt="image" src="https://github.com/user-attachments/assets/606e8a47-3531-4175-b7b9-e77e760329b4" />

El shell torna a indicar que hola no és una comanda executable. La captura il·lustra la diferència entre escriure text en un shell i escriure'l en un camp de text: per provar la descodificació cal teclejar en una aplicació o camp de text, no esperar que el shell tracti la frase com a text pla.

Comanda: sudo cat /tmp/test_es.log

Mostra el registre de la prova amb el mapa espanyol. La frase de prova apareix descodificada dins del fitxer, juntament amb les marques de tecles especials i les marques de temps.




Aquest serà el nostre script:

<img width="866" height="515" alt="image" src="https://github.com/user-attachments/assets/8bf7a93e-11fa-463c-982e-29ee35928ef8" />

Assignem permisos:
<img width="785" height="67" alt="image" src="https://github.com/user-attachments/assets/c3f2cf2d-694c-498f-ad0c-96d345971c73" />



Provem el script en segon pla:
<img width="940" height="99" alt="image" src="https://github.com/user-attachments/assets/df287ab7-cc84-48c5-9cc5-eea5ad744e2f" />

<img width="831" height="87" alt="image" src="https://github.com/user-attachments/assets/a3a4937c-ba6e-464a-a067-58c878e722cf" />

Comandes: sudo pkill -f logkeys i ps aux | grep logkeys

Atura la instància manual i comprova amb la llista de processos que no queda cap procés logkeys en execució, a banda del mateix grep.

<img width="831" height="87" alt="image" src="https://github.com/user-attachments/assets/00b11edc-77a3-4379-ad57-906439a9a48c" />
