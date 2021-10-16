# Beispiel-Suchapplikation

Dieses Projekt dient als Beispiel für Backend und Frontend einer Suchapplikation. Natürlich müssen Sie es nicht für Ihre Projekt verwenden,
es kann Ihnen aber etwas Arbeit am Anfang abnehmen. Falls Sie wollen, dürfen Sie selbstverständlich auch andere als die hier eingesetzten 
Technologien verwenden.

## Frontend

Das Frontend ist in Vue.js geschrieben. Eine genauere Beschreibung findet sich in [frontend/README.md](frontend/README.md).

## Backend 

Das Backend ist in Java geschrieben. Das Beispiel gibt unabhängig von der Anfrage immer nur ein JSON-Array mit zwei Strings zurück. Ihre Aufgabe hier
ist, die Anfrage des Frontends auf eine passende Anfrage an den ElasticSearch Cluster zu mappen (natürlich auch für die Antworten in die andere Richtung).

### Wozu ein zwischengelagerter Backend-Server?

Vielleicht haben Sie sich schon die Frage gestellt, warum überhaupt ein eigenes Backend nötig ist. Warum nicht einfach direkt den ElasticSearch-Cluster aus dem Frontend heraus ansprechen?

Für unser kleines Projekt wäre das eine valide Strategie. Allerdings wird durch einen weiteren vorgelagerten Server eine bessere Kapselung erzielt: Sobald z.B eine Authentifizierung notwendig ist, sollte dies ein extra Server übernehmen. Andernfalls müssten entsprechende Secrets clientseitig vorliegen, was keine gute Idee ist. Auch falls es strukturelle Änderungen der Daten in ElasticSearch gibt, muss lediglich das Mapping im Backend-Server angepasst werden, nicht aber im Frontend (was sich ja nur um die Darstellung kümmern sollte, die sich in diesem Fall nicht ändert).

Für unser Projekt sollten Sie die Anfrage vom Frontend möglichst einfach halten und die konkrete Abbildung auf ein ElasticSearch-Request im Backend vornehmen. Sie werden feststellen, dass letztere durchaus etwas aufwendiger werden können, sobald Sie neben dem eigentlich Suchwort auch noch einige Filter erlauben.
