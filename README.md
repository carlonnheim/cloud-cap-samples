# Demonstrates issue with global SELECT and non-singleton cds

The changes simulate a [**Reuse and Compose**](https://cap.cloud.sap/docs/guides/extensibility/composition) pattern by
* Separating modules so they have their own `node_modules` directories
* The `bookshop` is importing the `DataService` from `bookshop/db/schema.cds`
* The `bookshop/srv/cat-service.js` has a dummy operation before `READ` on `ListOfBooks` to use the global `SELECT` variable

To see the issue
```
(cd data-viewer && npm i)
cd bookshop
npm i
npx cds run # Now visit http://localhost:4004/browse/ListOfBooks
```

To make the issue go away, comment the imported reuse service in `bookshop/db/schema.cds`
```
...
// Reuse a service
//using { DataService } from '@capire/data-viewer/srv/data-service'; // <--- disable by commenting here
```

Then do `npx cds run` (from the bookshop directory) and visit the same url - now it works
