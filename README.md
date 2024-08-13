# mongoDB

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
   publishDate: { $gte: '1880' }
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
   $or: [
   { publishDate: { $lte: 1847 } },
   { categories: 'Classics' }
   ]
   });

10. db.getCollection('books').find({
    publishDate: { $lte: 'May' }
    });

11. db.collection.find({
    "title": 1,
    "isbn": 1,
    "\_id": 0
    })

12. db.collection.find({
    "author.firstName": 1,
    "author.lastName": 1,
    "\_id": 0
    })

13. db.movies.sort({ pages: 1 });

14. db.movies.sort({ pages: -1 });
