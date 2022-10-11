# mongodb

Означте метод підключення до екземпляра сервера MongoDB.

![image-20220810142606679](E:\san\AKIT\ДИСЦИП\Довідник Node-RED\NodREDGuide\storage_mongodb\media\image-20220810142606679.png)

Підтримуються 3 варіанти:        

- Standard/direct            
- Standard/replicaset 
- Clustered by DNS seedlist

**Connect options** – це місце, де ви додаєте додаткові параметри, необхідні для вашого екземпляра MongoDB. Це може включати:

- `w=majorityreplica`
- `Set=replset`
- `authSource=admin`

та будь-які інші відповідні варіанти - повний комплект доступний за адресою  [Connection String URI Format — MongoDB Manual](https://docs.mongodb.com/manual/reference/connection-string/).   

Якщо ви підключаєтеся до [IBM Databases for MongoDB](https://cloud.ibm.com/catalog/services/databases-for-mongodb-group), як набір реплік, обов’язково додайте в **Connect options**   `ssl=true&tlsAllowInvalidCertificates=true `  .



# mongodb out

Простий вихідний вузол MongoDB. Може зберігати, вставляти, оновлювати та видаляти об’єкти з вибраної колекції.  

![image-20220810142741815](E:\san\AKIT\ДИСЦИП\Довідник Node-RED\NodREDGuide\storage_mongodb\media\image-20220810142741815.png)

Оновлення змінює існуючий об’єкт чи об’єкти. Запит на вибір об’єктів для оновлення використовує `msg.query`, а оновлення елемента використовує `msg.payload`. Якщо `msg.query._id` є дійсним рядком mongo ObjectId, його буде перетворено на тип ObjectId.



Update can add a object if it does not exist or update multiple objects.    

Remove will remove objects that match the query passed in on `msg.payload`. A blank query will delete    *all of the objects* in the collection.    

You can either set the collection method in the node config or on `msg.collection`. Setting it in the    node will override `msg.collection`.    

By default MongoDB creates an *_id* property as the primary key - so repeated injections of the    same `msg` will result in many database entries.    

If this is NOT the desired behaviour - ie. you want repeated entries to overwrite, then you must set    the `msg._id` property to be a constant by the use of a previous function node.    

This could be a unique constant or you could create one based on some other msg property.    

Currently we do not limit or cap the collection size at all... this may well change.

# mongodb in

Calls a MongoDB collection method based on the selected operator.    

![image-20220810142811500](E:\san\AKIT\ДИСЦИП\Довідник Node-RED\NodREDGuide\storage_mongodb\media\image-20220810142811500.png)

Find queries a collection using the `msg.payload` as the query statement as per the .find() function.    Optionally, you may also (via a function) set a `msg.projection` object to constrain the returned    fields, a `msg.sort` object, a `msg.limit` number and a `msg.skip` number.    

Count returns a count of the number of documents in a collection or matching a query using the    `msg.payload` as the query statement.    

Aggregate provides access to the aggregation pipeline using the `msg.payload` as the pipeline array.    

You can either set the collection method in the node config or on `msg.collection`. Setting it in    the node will override `msg.collection`.    

See the [*MongoDB     collection methods docs*](http://docs.mongodb.org/manual/reference/method/db.collection.find/) for examples.    

The result is returned in `msg.payload`.