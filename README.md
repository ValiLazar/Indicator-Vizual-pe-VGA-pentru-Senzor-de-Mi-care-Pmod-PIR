# Indicator Vizual pe VGA pentru Senzor de Miscare Pmod-PIR

📝 Descriere Generală
Acest proiect demonstrează o aplicație practică de integrare a unui senzor extern cu o placă FPGA pentru a oferi feedback vizual pe un monitor. Sistemul funcționează ca un indicator de securitate sau prezență, schimbând culoarea întregului ecran în funcție de starea unui senzor de mișcare infraroșu (PIR).

Designul este conceput pentru o placă Digilent Basys 3 și un Pmod PIR, generând un semnal video stabil la rezoluția 1920x1080 (Full HD).

🚦 Funcționalitate
Logica sistemului este directă și se bazează pe starea semnalului de intrare de la senzor:


Fără Mișcare Detectată: Când intrarea Motion_detected este pe nivel logic 0, modulul Pmod_PIR setează culoarea ecranului la verde.


Mișcare Detectată: Când senzorul detectează mișcare și setează intrarea Motion_detected pe 1, modulul schimbă instantaneu culoarea ecranului în roșu.


Afișaj Oprit: În afara zonei vizibile a ecranului (în timpul perioadelor de blanking), toate ieșirile de culoare sunt setate pe negru pentru a respecta standardul VGA.

📁 Structura Proiectului
Proiectul este modular, fiecare fișier având o responsabilitate clară:


vga_top.v: Modulul principal care integrează toate componentele. Acesta instanțiază un 

Clocking Wizard pentru a genera ceasul de 148.5 MHz , controlerul de temporizare VGA și modulul de logică pentru senzor. De asemenea, conectează portul de intrare 

Motion_detected la logica internă.


vga_1920X1080.v: Un controler de temporizare VGA care generează semnalele de sincronizare h_sync și v_sync pentru o rezoluție de 1920x1080 pixeli. Acesta informează restul sistemului când se află în zona de afișare activă prin semnalul 
display_on.


Pmod_PIR.v: Conține logica principală a aplicației. Primește semnalul 

Motion_detected și, în funcție de valoarea acestuia, setează ieșirile de culoare vgaRed, vgaGreen și vgaBlue.


Basys3_Master.xdc: Fișierul de constrângeri care mapează porturile din vga_top.v la pinii fizici ai plăcii Basys 3. Cel mai important, mapează intrarea Motion_detected la pinul J1, corespunzător primului pin al conectorului Pmod JA.
