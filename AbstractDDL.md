# What do we need to have an abstract DDL library

# API #
  * create\_table(name, options)
  * drop\_table(name)
  * rename\_table(old\_name, new\_name)
  * add\_column(table\_name, column\_name, type, options)
  * rename\_column(table\_name, column\_name, new\_column\_name)
  * change\_column(table\_name, column\_name, type, options)
  * remove\_column(table\_name, column\_name)
  * add\_index(table\_name, column\_name, index\_type)
  * remove\_index(table\_name, column\_name)