## Beschreibung der GOT

| Index | Adresse    | Name       | Typ      |
|-------|------------|------------|----------|
| ...   | ...        | ...        | ...      |
| 12    | 0x00906472 | CreateHeap | Funktion |
| 13    | 0x00903438 | HeapAlloc  | Funktion |
| ...   | ...        | ...        | ...      |

## Aufruf von CreateWindow
Wir  wollen CreateWindow aufrufen, dazu müssen wir die Adresse aus der GOT lesen und anspringen. Dazu wird zuerst die Adresse der GOT geladen, man läd den aktuellen instruction pointer (eip) mit | call LABEL | LABEL: pop ebx | in ebx und subtrahiert die relative Position, von der aus wir den eip gelesen haben. Jetzt haben wir die Startadresse des Moduls in ebx. Zuletzt muss noch der GOT_OFFSET hinzugefügt werden. Der Index unsere Funktion ist 0x20, das heißt mit call [ebx+0x20*4] kann diese angesprungen werden. In CreateWindow wird HeapAlloc aufgerufen, dazu wird wieder die Adresse der GOT in ebx geladen und HeapAlloc mit call [ebx+0x13*4] angesprungen. Beim verlassen beider Funktionen wird der alte Wert von ebx wiederhergestellt.

