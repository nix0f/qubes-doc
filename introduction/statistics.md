---
lang: it
layout: site
permalink: /statistics/
redirect_from:
- /counter/
ref: 127
title: Statistics
---

<div class="center-block more-bottom">
  <a href="https://tools.qubes-os.org/counter/stats.png">
    <img src="https://tools.qubes-os.org/counter/stats.png" alt="Estimated Qubes OS userbase graph"/>
  </a>
</div>

## FAQ

### Con quale frequenza viene aggiornato questo grafico?

Giornalmente.

### Perché la barra del mese corrente è così bassa?

Visto che il grafico viene aggiornato quotidianamente, la barra del mese corrente sarà molto bassa all'inizio del mese e aumenterà gradualmente fino alla fine del mese.

### Come viene stimata la base utenti?

Contiamo semplicemente il numero di indirizzi IPv4 univoci che si connettono ai server di aggiornamento di Qubes ogni mese (ad eccezione delle connessioni Tor; vedi [sotto](#how-are-tor-users-counted)). (Nota: gli utenti che hanno configurato manualmente i propri sistemi per bypassare il metalink e connettersi direttamente a un mirror non vengono conteggiati.)

### Come vengono conteggiati gli utenti Tor?

Stimiamo il numero di utenti Tor quale proporzione del numero totale di *richieste* dai nodi di uscita Tor partendo dal presupposto che la proporzione di utenti rispetto alle richieste sia più o meno la stessa sia per gli utenti Clearnet che per quelli Tor.
Per essere precisi la formula è:

```
tor_users = tor_requests * (plain_users / plain_requests)
```

Dove:

- `tor_users` è il numero stimato di utenti Qubes che scaricano aggiornamenti tramite Tor ogni mese.
- `tor_requests` è il numero totale di richieste che i server di aggiornamento Qubes ricevono dai nodi di uscita Tor ogni mese.
- `plain_users` è il numero di indirizzi IPv4 clearnet univoci che si collegano ogni mese ai server di aggiornamento di Qubes.
- `plain_requests` è il numero totale di richieste che i server di aggiornamento Qubes ricevono ogni mese dagli indirizzi IPv4 clearnet.

We cross-reference the list of connecting IP addresses with [TorDNSEL's exit lists](https://metrics.torproject.org/collector.html#type-tordnsel) in order to distinguish Tor and clearnet IPs and requests.
For this purpose, we count an IP address as belonging to a Tor exit node if there was a Tor exit node active for that address within the 24-hour periods before or after it connected to the Qubes update servers.

### Che tipo di dati raccogliete sugli utenti di Qubes?

Consulta la nostra [Privacy Policy](/privacy/).

### Dove posso trovare i dati grezzi e il codice sorgente?

I dati grezzi sono disponibili [qui](https://tools.qubes-os.org/counter/stats.json).
(Non includono dati o riferimenti agli utenti)
Il formato di questi dati non è documentato e può cambiare in qualsiasi momento se gli sviluppatori sentono la necessità di includere altri campi.
Il codice corgente è disponibilie  [qui](https://github.com/woju/qubes-stats).
