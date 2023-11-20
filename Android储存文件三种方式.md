# Android储存文件基本三种方式：

| 文件                                                         | SharedPreferences储存                                    | 数据库储存                              |
| ------------------------------------------------------------ | -------------------------------------------------------- | --------------------------------------- |
| 适合用于存储一些简单的文本数据或二进制数据。                 | Context类中的**getSharedPreferences**()方法              | LitePal                                 |
| Context类中提供了一个**openFileOutput**()方法，可以用于将数据存储到指定的文件中。 | Activity类中的**getPreferences**()方法                   | SQLite数据库                            |
| Context类中还提供了一个**openFileInput**()方法，用于从文件中读取数据 | PreferenceManager类中的getDefaultSharedPreferences()方法 | 相比之下，我认为LitePal更为适合实际使用 |
