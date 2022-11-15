# No SQL Dökümantasyon Veri tabanı (MongoDB)

### Veritabanı yönetimi

**use databaseName**: Veritabanı oluşturur veya kullanır.

```bash
use <databaseName>
```

**db.dropDatabase()** : Veritabanını siler.

```bash
db.dropDatabase()
```

**db.collection.drop()** : Belirtilen koleksiyonu siler.

```bash
db.<collection_name>.drop()
```

**db.collection.dropIndex({key:value})** : Belirtilen indeksi siler.

```bash
db.<collection_name>.dropIndex({<key>:<value>})
```

**db.collection.renameCollection(new_collection_name)** : Belirtilen koleksiyonun adını değiştirir.

```bash
db.<collection_name>.renameCollection(<new_collection_name>)
```

**db.collection.stats()** : Belirtilen koleksiyonun istatistiklerini getirir.

```bash
db.<collection_name>.stats()
```

**db.collection.count()** : Belirtilen koleksiyonun kayıt sayısını getirir.

```bash
db.<collection_name>.count()
```

**db.collection.distinct(key)** : Belirtilen key'in değerlerini getirir.

```bash
db.<collection_name>.distinct(<key>)
```

```bash
db.createCollection("<collection_name>")
```

### Kayıt ekleme

**db.collection.insertOne()** : Tek bir kayıt ekler.

```bash
db.<collection_name>.insertOne({<key>:<value>})
```

**db.collection.insertMany()** : Birden fazla kayıt ekler.

```bash
db.<collection_name>.insertMany([{<key>:<value>},{<key>:<value>}])
```

**db.collection.insert()** : Tek bir kayıt ekler veya birden fazla kayıt ekler.

```bash
db.<collection_name>.insert({<key>:<value>})
```

### Kayıtları getirme

**db.collection.find()** : Tüm kayıtları getirir.

```bash
db.<collection_name>.find()
```

**db.collection.find({key:value})** : Belirtilen key ve value değerine sahip kayıtları getirir.

```bash
db.<collection_name>.find({<key>:<value>})
```

**db.collection.find({key:{$in:[value1,value2]}})** : Belirtilen key ve value değerlerine sahip kayıtları
getirir.

```bash
db.<collection_name>.find({<key>:<{$in:[<value1>,<value2>]>}})
```

**db.collection.find({key:value},{key:value})** : Belirtilen key ve value değerine sahip kayıtları getirir.

```bash
db.<collection_name>.find({<key>:<value>},{<key>:<value>})
```

**db.collection.find({key:{$gt:value}})** : Belirtilen key değerinden büyük kayıtları getirir.

```bash
db.<collection_name>.find({<key>:{$gt:<value>}})
```

**db.collection.find({key:{$gte:value}})** : Belirtilen key değerinden büyük veya eşit kayıtları getirir.

```bash
db.<collection_name>.find({<key>:{$gte:<value>}})
```

**db.collection.find({key:{$lt:value}})** : Belirtilen key değerinden küçük kayıtları getirir.

```bash
db.<collection_name>.find({<key>:{$lt:<value>}})
```

**db.collection.find({key:{$or:[{key:value},{key:value}]}})** : Belirtilen key değerlerinden birini içeren
kayıtları getirir.

```bash
db.<collection_name>.find({<key>:{$or:[{<key>:<value>},{<key>:<value>}]}})
```

**db.collection.find({key:value}).limit(value)** : Belirtilen key ve value değerine sahip kayıtlarını limite göre
getirir.

```bash
db.<collection_name>.find({<key>:<value>}).limit(<value>)
```

**db.collection.find({key:value}).sort({key:value})** : Belirtilen key ve value değerine sahip kayıtları
sıralar.

```bash
db.<collection_name>.find({<key>:<value>}).sort({<key>:<value>})
```

**db.collection.find({key:value}).count()** : Belirtilen key ve value değerine sahip kayıtların sayısını getirir.

```bash
db.<collection_name>.find({key:value}).count()
```

### İç içe dökümanlar

**db.collection.find({key.key:value})** : Belirtilen key'in içindeki key ve value değerine sahip kayıtları getirir.

```bash
db.<collection_name>.find({<key.subkey>:<value>})
```

### Dizi içinde arama

**db.collection.find({key:[value,value]})** : Belirtilen key'in içinde sadece belirtilen değerleri içeren
kayıtları getirir.

```bash
db.<collection_name>.find({<key>:[<value1>,<value2>]})
```

**db.collection.find({key:[{$all:[value,value]}]})** : Belirtilen key'in içinde belirtilen değerleri içeren tüm
kayıtları getirir.

```bash
db.<collection_name>.find({
  <key>:[{$all:[<value1>,<value2>]}]
  })
```

**db.collection.find({key:{$elemMatch:{key:value}}})** : Belirtilen key'in içinde belirtilen değerleri içeren tüm
kayıtları getirir.

```bash
db.<collection_name>.find({
  <key>:{$elemMatch:{<key>:<value>}}
  })
```

### Projeleme

**db.collection.find({key:value},{key:value})** : Sadce belirtilen key ve value değerine sahip kayıtların
belirtilen kolonlarını getirir.

```bash
db.<collection_name>.find({<key>:<value>},{<key>:1})

# 1 : true, 0 : false
db.<collection_name>.find({<key>:<value>},{<key>:0}) 
```

### Bulunmayan kayıtları getirme

**db.collection.find({key:null})** : Değerleri null olan kayıtları getirir.

```bash
db.<collection_name>.find({<key>:null})
```

**db.collection.find({key:{$type:value}})** : Belirtilen key'in değerinin tipine göre kayıtları getirir.

Veri tipi için [tıklayınız](https://docs.mongodb.com/manual/reference/operator/query/type/).

```bash
db.<collection_name>.find({
  <key>:{$type:<value>}
  })
```

**db.collection.find({key:{$exists:value}})** : Belirtilen key'in değerinin varlığına göre kayıtları getirir.

```bash
# true, false
db.<collection_name>.find({
  <key>:{$exists:true}
  })

db.<collection_name>.find({
  <key>:{$exists:false}
  })
```

### Kayıtları güncelleme

**db.collection.updateOne** : Belirtilen kaydı günceller.

```bash
db.<collection_name>.updateOne({
  <key>:<value>},{
    $set{<key>:<value>},$currentDate{lasetModified:true}
    }
)
```

**db.collection.updateMany** : Birden fazla kaydı günceller.

```bash
db.<collection_name>.updateMany({
  <key>:<value>},{
    $set{<key>:<value>},
    $currentDate{lasetModified:true}}
)
```

**db.collection.replaceOne** : Belirtilen kaydı belirtilen değerlerle değiştirir.

```bash
db.<collection_name>.replaceOne({
  <key>:<value>},{
    <key>:<value>}
)
```

### Kayıtları silme

**db.collection.deleteOne** : Belirtilen kaydı siler.

```bash
db.<collection_name>.deleteOne({<key>:<value>})
```

**db.collection.deleteMany** : Birden fazla kaydı siler.

```bash
# Tüm kayıtları siler.
db.<collection_name>.deleteMany({})

# Belirtilen key ve value değerine sahip kayıtları siler.

db.<collection_name>.deleteMany(<key>:<value>})
```

### Bulk işlemleri

**db.collection.bulkWrite** : Birden fazla işlemi tek seferde yapar.

insertOne: Belirtilen kaydı ekler.

```bash
db.<collection_name>.bulkWrite([
  {insertOne:{<key>:<value>}}
])
```

updateOne: Belirtilen kaydı günceller.

```bash
db.<collection_name>.bulkWrite([
  {updateOne:{<key>:<value>}}
])
```

deleteOne: Belirtilen kaydı siler.

```bash
db.<collection_name>.bulkWrite([
  {deleteOne:{<key>:<value>}}
])
```

Tüm işlemleri tek seferde yapmak için:

```bash
db.<collection_name>.bulkWrite([
  {insertOne:{<key>:<value>}},
  {updateOne:{<key>:<value>}},
  {deleteOne:{<key>:<value>}}
])
```

### Metinin içinde arama

**db.collection.find({$text:{$search:"value"}})** : Tüm verilerde belirtilen değeri arar.

```bash
db.<collection_name>.find({
  $text:{$search:"<value>"}
  })
```

### Coğrafi sorgulama

GeoJSON formatında verileri aramak
için [tıklayınız](https://docs.mongodb.com/manual/reference/operator/query-geospatial/).

**db.collection.createIndex({key:value})** : Belirtilen key'e göre indeks oluşturur.

```bash
db.<collection_name>.createIndex({<key>:<value>})
```

**db.collection.find({locationField:{$geoIntersects:{$geometry:{key:value}}}})** : Belirtilen key'in değerinin
belirtilen key'in değerine göre kesiştiği kayıtları getirir.

```bash
db.<collection_name>.find({
  <locationField>:{
    $geoIntersects:{
      $geometry:{<key>:<value>}}
      }
  })
```

**db.collection.find({locationField:{$geoWithin:{$geometry:{key:value}}}})** : Belirtilen key'in değerinin
belirtilen alan içerisinde olduğu kayıtları getirir.

```bash
db.<collection_name>.find({
  <locationField>:{
    $geoWithin:{
      $geometry:{<key>:<value>}}
      }
  })
```

**db.collection.find({locationField:{$near:{$geometry:{key:value}}}})** : Belirtilen key'in değerinin belirtilen
key'in değerine göre yakınlığına göre kayıtları getirir.

```bash
# minDistance: Belirtilen değerden büyük olan kayıtları getirir.
# maxDistance: Belirtilen değerden küçük olan kayıtları getirir.

db.<collection_name>.find({
  <locationField>:{$near:{
    $geometry:{<key>:<value>},
    $minDistance:<value>,
    $maxDistance:<value>}}
    })
```

### Aggregation (Gruplama, toplama, sıralama, filtreleme, sayma) işlemleri

**db.collection.aggregate([{$group:{_id:key,key:{$value:key}}},{$sort:{key:value}}])** : Önce belirtilen key'e göre
gruplama yapar, sonra da belirtilen key'e göre sıralama yapar.

```bash
# $sort: 1 (Artan), -1 (Azalan)
db.<collection_name>.aggregate([
  {$group:{_id:<key>,<key>:{$<value>:<key>}}},
  {$sort:{<key>:-1}}
  ])
```

Diğer stage'ler için [tıklayınız](https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/).

## MongoDB Java Entegrasyonu

Java indirmek için [tıklayınız](https://www.oracle.com/java/technologies/javase-downloads.html).

MongoDB Java driver dependency:

```xml

<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongo-java-driver</artifactId>
    <version>3.12.7</version>
</dependency>
```

MongoDB Java driver dokümantasyonu
için [tıklayınız](https://mongodb.github.io/mongo-java-driver/3.12/driver/getting-started/quick-start/).
