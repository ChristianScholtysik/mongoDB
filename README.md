# mongoDB

## MongoDB-Query-2-1

1. Bücher, die von Jane Austen geschrieben wurden
2. Bücher mit mehr als 500 Seiten an
3. Bücher, die nach 1880 veröffentlich wurden
4. Bücher, deren Sprache Englisch ist
5. Bücher, die höher als 8 Inches sind
6. Bücher mit den Kategorien „Classic“ oder „Romance“
7. Bücher, deren Herausgeber (publisher) “Books” im Namen hat
8. Bücher, bei denen der Vorname der/s Autor:in mit “J” beginnt
9. Bücher, die 1847 oder früher veröffentlicht wurden und die Kategorie „Classic“ haben
10. Bücher, die zwischen Januar und Mai veröffentlicht wurden
11. Nur Titel und ISBN der Bücher
12. Nur die Vor- und Nachnamen der Autor:innen ohne weitere Informationen
13. Bücher sortiert nach Seitenanzahl aufsteigend
14. Bücher sortiert nach Seitenanzahl absteigend

Antworten:

1. db.getCollection('books').find({
   'author.firstName': 'Jane',
   'author.lastName': 'Austen'
   });

2. db.getCollection('books').find({
   pages: { $gte: '500' }
   });

3. db.getCollection('books').find({
   publishDate: { $gte: '1881' }
   });

4. db.getCollection('books').find({
   language: 'English'
   });

5. db.getCollection('books').find({
   'dimensions.height': { $gte: '8.0 inches' }
   });

6. db.getCollection('books').find({
   $or: [
   { categories: 'Classics' },
   { categories: 'Romance' }
   ]
   });

7. db.getCollection('books').find({
   publisher: RegExp('Books')
   });

8. db.getCollection('books').find({
   'author.firstName': RegExp('J')
   });

9. db.getCollection('books').find({
   publishDate: { $lte: '1847' },
   categories: 'Classic'
   });

10. db.getCollection('books').find({
    publishDate: { $lte: 'May' }
    });

11. db.getCollection('books').find(
    {},
    { title: 1, isbn: 1, \_id: 0 }
    );

12. db.getCollection('books').find(
    {},
    {
    'author.firstName': 1,
    'author.lastName': 1,
    \_id: 0
    }
    );

13. db.movies.sort({ pages: 1 });

14. db.movies.sort({ pages: -1 });

## MongoDB-Query-3-1

Ziel: Daten in einer in MongoDB Collection filtern und auswerten

Wir bauen auf [MongoDB-Query-2-1](https://www.notion.so/MongoDB-Query-2-1-0bb38225e58a40238d1862457e7247e5?pvs=21) auf

- Lege zwei eigene Bücher an, bei denen du nicht alle Felder angibst
- Schau dir die Bücher danach in der Übersicht an

Du sollst einige schwierigere Queries/Abfragen für folgende Anwendungsfälle erstellen.

Speichere die Abfragen in einer Textdatei und lade sie in deinem Repository hoch

1. Bücher, die entweder von Jane Austen oder Charlotte Brontë stammen und nach 1840 veröffentlicht wurden
2. Bücher, die in den letzten 100 Jahren veröffentlicht wurden und entweder die Kategorie „Classic“ oder „Romance“ haben
3. Bücher mit Seitenanzahl zwischen 200 und 500, die von „Charles Dickens“ geschrieben wurden
4. Bücher von „Herman Melville“ oder „Mary Shelley“, die als Hardcover oder E-Book verfügbar sind
5. Bücher, die in der Kategorie „Gothic Fiction“ veröffentlicht wurden, sortiert nach der Seitenanzahl in absteigender Reihenfolge
6. Bücher, die in mindestens zwei verschiedenen Formaten verfügbar sind, veröffentlicht vor 1850 und die Kategorie „Adventure“ haben
7. Bücher, deren Titel mit „The“ beginnt und die mehr als 400 Seiten haben oder in der Kategorie „Classic“ sind
8. Durchschnittliche Seitenanzahl für Bücher, die nach 1900 veröffentlicht wurden

# ☝🏼 Hinweis

- Schau dir auf jeden Fall aggregate ($match, $group), $and und $or an

1. db.getCollection('books').find({
   $and: [
   {
   'author.firstName': 'Jane',
   'author.lastName': 'Austen'
   },
   {
   'author.firstName': 'Charlotte',
   'author.lastName': 'Brontë'
   },
   { publishDate: { $gte: '1840' } }
   ]
   });

2. db.getCollection('books').find({
   $and: [
   { publishDate: { $gte: '1924' } },
   {
   $or: [
   { categories: 'Classics' },
   { categories: 'Romance' }
   ]
   }
   ]
   });
