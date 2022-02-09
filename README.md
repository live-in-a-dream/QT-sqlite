# QT-sqlite

Qt的sqlite加密.


    const QString driverName = "SQLITECIPHER";
    QPluginLoader driverload("./sqlitecipher.dll");
    if(driverload.load())
    {
        sqlPlugin = qobject_cast<QSqlDriverPlugin*>(driverload.instance());
        if(sqlPlugin){
            driver=sqlPlugin->create(driverName);
            Log::d("Sqlite获取插件成功!");
        }else{
            Log::d("Sqlite获取插件失败!");
        }
    }
    Log::d("Sqlite加密插件失败!");



    QSqlQuery* MySqlite::GetQSqlQuery(){
        if(driver != nullptr && qSqlQuery == nullptr){
            QSqlDatabase db = QSqlDatabase::addDatabase(driver);
            db.setDatabaseName(dbName);
            db.setPassword("123456");
            if(db.open())
            {
                qSqlQuery = new QSqlQuery(db);
                return qSqlQuery;
            }
        }
        return qSqlQuery;
    }
