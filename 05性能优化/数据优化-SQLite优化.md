### 一，概述
Android中对于SQLite数据库的操作，系统为我们提供了很方便的实现。我们只需要创建自己的一个类继承SQLiteOpenHelper类并实现其中的onCreate方法和onUpgrade方法即可。
优化可以从如下两方面进行： 事务和索引。


### 二，优化一---事务
#### 2.1 事务介绍
对于事务，就是数据库的一次原子性的执行操作。原子性的执行操作为数据的整体性执行带来的可靠安全性。在SQLite中，如果我们默认事务(会为每个插入和更新都创建一次事务，并且在每次插入和更新后会立刻提交本次操作)，即没有手动创建事务，假设此时有1000条数据，那么数据的执行流程是 创建事务 -> 执行插入或更新操作 -> 提交事务，这样的流程会执行1000次。如果我们手动创建了事务，则执行流程为: 创建事务 -> 执行1000条SQL数据操作 -> 提交事务。很明显，我们在SQLite中使用事务可以为插入和更新操作带来很大的优化。

#### 2.2 具体实例
      /**01 开启事务**/
      sqLiteDatabase.beginTransaction();
      try {
          for (int i = 0; i < 100; i++) {
              ContentValues contentValues = new ContentValues();
              contentValues.put("name", "test" + i);
              sqLiteDatabase.insertOrThrow(table, null, contentValues);
          }
          /**02 将数据库事务设置为成功**/
          sqLiteDatabase.setTransactionSuccessful();
      } catch (Exception e) {
          e.printStackTrace();
      } finally {
          /**03 结束数据库事务**/
          sqLiteDatabase.endTransaction();
      }

### 三，优化二---索引
#### 3.1 概述
索引（Index）是一种特殊的查找表，数据库搜索引擎用来加快数据检索。简单地说，索引是一个指向表中数据的指针。一个数据库中的索引与一本书后边的索引是非常相似的。

#### 3.2 使用索引注意点
- 索引不应该使用在较小的表上。
- 索引不应该使用在有频繁的大批量的更新或插入操作的表上。
- 索引不应该使用在含有大量的 NULL 值的列上。
- 索引不应该使用在频繁操作的列上。

### 四，其他优化细节
- 01）使用StringBuilder或StringBuffer来拼接字符串：SQL语句字符串的拼接或创建多个临时变量，此时我们可以使用StringBuilder或StringBuffer来拼接字符串。
- 02）cursor使用后要及时关闭：即在查询完结果后，调用cursor.close()将资源关闭。
