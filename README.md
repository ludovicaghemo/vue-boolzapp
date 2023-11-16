# CONSEGNA

**Milestone 1**
- [x] Replica della grafica con la possibilità di avere messaggi scritti dall’utente (verdi) e
dall’interlocutore (bianco) assegnando due classi CSS diverse
- [x] Visualizzazione dinamica della lista contatti: tramite la direttiva v-for, visualizzare nome e immagine di ogni contatto

**Milestone 2**
- [x] Visualizzazione dinamica dei messaggi: tramite la direttiva v-for, visualizzare tutti i messaggi relativi al contatto attivo all’interno del pannello della conversazione
- [x] Click sul contatto mostra la conversazione del contatto cliccato

**Milestone 3**
- [] Aggiunta di un messaggio: l’utente scrive un testo nella parte bassa e digitando
“enter” il testo viene aggiunto al thread sopra, come messaggio verde
- [] Risposta dall’interlocutore: ad ogni inserimento di un messaggio, l’utente riceverà
un “ok” come risposta, che apparirà dopo 1 secondo.

**Milestone 4**
- [] Ricerca utenti: scrivendo qualcosa nell’input a sinistra, vengono visualizzati solo i
contatti il cui nome contiene le lettere inserite (es, Marco, Matteo Martina -> Scrivo
“mar” rimangono solo Marco e Martina)

**Milestone 5 - opzionale**
- [] Cancella messaggio: cliccando sul messaggio appare un menu a tendina che
permette di cancellare il messaggio selezionato
- [] Visualizzazione ora e ultimo messaggio inviato/ricevuto nella lista dei contatti


# Soluzione

**MILESTONE 1**
Visualizzazione dinamica della lista contatti: tramite la direttiva v-for, visualizzare
nome e immagine di ogni contatto


```
<ul class="chats-list">
                                <!-- Lista chat e contatti inseriti dinamicamente -->
                                <li class="single-chat flex" v-for="(singleContact, index) in contacts">
                                    <div class="flex">
                                        <button class="btn profile-pic-btn">
                                            <img :src="`img/avatar${singleContact.avatar}.jpg`" alt="">
                                        </button>
                                        <div class="chat-info">
                                            <h6 class="contact">{{singleContact.name}}</h6>
                                            <p class="chat-preview">Lorem ipsum dolor sit amet</p>
                                        </div>
                                    </div>
                                    <div class="time chat-time">16:15</div>
                                </li>
                            </ul>
```

**Milestone 2**
Visualizzazione dinamica dei messaggi: tramite la direttiva v-for, visualizzare tutti i
messaggi relativi al contatto attivo all’interno del pannello della conversazione.
Click sul contatto mostra la conversazione del contatto cliccato:

1. Impostare activeContactIndex = 0 per tenere traccia del contatto attivo;  
2. Impostare @click="setActiveContact(singleContact)" ai singoli contatti delle chat;
3. setActiveContact(singleContact) = funzione per impostare il contatto attivo

    ```
     methods: {
        setActiveContact: function(singleContact) {
            this.activeContactIndex = singleContact;
        }
    }
    ```
4. Tramite v-for visualizzare i messaggi relativi al contatto attivo

```
<div class="main-text flex" v-for="(curMessage, index) in activeContactIndex.messages" :key="index">
                                <div class="text" :class="curMessage.status === 'sent' ? 'sent' : 'received'">
                                    <div class="angle">
                                        <i class="fa-solid fa-angle-down"></i>
                                    </div>
                                    <div class="text-info">
                                        <ul>
                                            <li>Info messaggio</li>
                                            <li>Cancella messaggio</li>
                                        </ul>
                                    </div>
                                    <p class="text-message">
                                        {{curMessage.message}}
                                    </p>
                                    <div class="time text-time">{{curMessage.date}}</div>
                                </div>
                            </div>
```