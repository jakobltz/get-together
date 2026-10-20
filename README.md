# get-together

Einladungsseite, die Zu- und Absagen einsammelt. Eine statische HTML-Datei auf
GitHub Pages, die Antworten per REST in eine Supabase-Tabelle schreibt.

## Links

- Köln: `https://jakobltz.github.io/get-together/?e=koeln`
- Frankfurt: `https://jakobltz.github.io/get-together/?e=frankfurt`

Das Event kommt aus dem Query-Parameter `e`. Ohne Parameter greift `koeln`.

## Neues Event anlegen

In `index.html` im Objekt `EVENTS` einen Eintrag ergänzen (Stadt, Titel, Wann,
Wo, Hinweiszeile) und denselben Schlüssel in der Supabase-Policy unter
`event_id in (...)` zulassen. Sonst weist die Datenbank die Antwort ab.

## Datenhaltung

Tabelle `public.rsvp`: `event_id`, `name`, `attending`, `guests`, `note`,
`created_at`.

Row Level Security ist aktiv und erlaubt der Rolle `anon` ausschließlich
`insert`. Es gibt bewusst **keine** Leseregel: Wer den Link hat, kann antworten,
aber nicht sehen, wer sonst zugesagt hat. Der Publishable Key in `index.html`
ist dafür gemacht, öffentlich zu stehen — der Schutz liegt in der Policy, nicht
im Schlüssel. Ausgelesen wird der Stand über einen Access Token, der nicht in
diesem Repo liegt.
