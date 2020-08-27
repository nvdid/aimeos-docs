
# currency
## decorators/excludes

Excludes decorators added by the "common" option from the locale currency manager

```
mshop/locale/manager/currency/decorators/excludes = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the locale currency manager.

```
 mshop/locale/manager/currency/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the locale currency manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/currency/decorators/global
* mshop/locale/manager/currency/decorators/local

## decorators/global

Adds a list of globally available decorators only to the locale currency manager

```
mshop/locale/manager/currency/decorators/global = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the locale currency
manager.

```
 mshop/locale/manager/currency/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the locale
currency manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/currency/decorators/excludes
* mshop/locale/manager/currency/decorators/local

## decorators/local

Adds a list of local decorators only to the locale currency manager

```
mshop/locale/manager/currency/decorators/local = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Locale\Manager\Currency\Decorator\*") around the locale
currency manager.

```
 mshop/locale/manager/currency/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Locale\Manager\Currency\Decorator\Decorator2" only to the
locale currency manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/currency/decorators/excludes
* mshop/locale/manager/currency/decorators/global

## name

Class name of the used locale currency manager implementation

```
mshop/locale/manager/currency/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default locale currency manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Locale\Manager\Currency\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Locale\Manager\Currency\Mycurrency
```

then you have to set the this configuration option:

```
 mshop/locale/manager/currency/name = Mycurrency
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyCurrency"!


## standard/count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/currency/standard/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloccu."id"
 	FROM "mshop_locale_currency" AS mloccu
 	WHERE :cond
 	ORDER BY mloccu."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/locale/manager/currency/standard/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/currency/standard/insert/ansi
* mshop/locale/manager/currency/standard/update/ansi
* mshop/locale/manager/currency/standard/delete/ansi
* mshop/locale/manager/currency/standard/search/ansi

## standard/count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/currency/standard/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloccu."id"
 	FROM "mshop_locale_currency" AS mloccu
 	WHERE :cond
 	ORDER BY mloccu."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloccu."id"
 	FROM "mshop_locale_currency" AS mloccu
 	WHERE :cond
 	ORDER BY mloccu."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/locale/manager/currency/standard/count/ansi

## standard/delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/currency/standard/delete/ansi = 
 DELETE FROM "mshop_locale_currency" WHERE :cond
```

* Default: mshop/locale/manager/currency/standard/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the language records specified by the given IDs from the
locale database. The records must be from the site that is configured
via the context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/currency/standard/insert/ansi
* mshop/locale/manager/currency/standard/update/ansi
* mshop/locale/manager/currency/standard/search/ansi
* mshop/locale/manager/currency/standard/count/ansi

## standard/delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/currency/standard/delete/mysql = 
 DELETE FROM "mshop_locale_currency" WHERE :cond
```

* Default: 
 DELETE FROM "mshop_locale_currency" WHERE :cond


See also:

* mshop/locale/manager/currency/standard/delete/ansi

## standard/insert/ansi

Inserts a new currency record into the database table

```
mshop/locale/manager/currency/standard/insert/ansi = 
 INSERT INTO "mshop_locale_currency" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/locale/manager/currency/standard/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the currency item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the saveItems() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/currency/standard/update/ansi
* mshop/locale/manager/currency/standard/delete/ansi
* mshop/locale/manager/currency/standard/search/ansi
* mshop/locale/manager/currency/standard/count/ansi

## standard/insert/mysql

Inserts a new currency record into the database table

```
mshop/locale/manager/currency/standard/insert/mysql = 
 INSERT INTO "mshop_locale_currency" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_locale_currency" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )


See also:

* mshop/locale/manager/currency/standard/insert/ansi

## standard/search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/currency/standard/search/ansi = 
 SELECT :columns
 	mloccu."id" AS "locale.currency.id", mloccu."label" AS "locale.currency.label",
 	mloccu."status" AS "locale.currency.status", mloccu."mtime" AS "locale.currency.mtime",
 	mloccu."editor" AS "locale.currency.editor", mloccu."ctime" AS "locale.currency.ctime"
 FROM "mshop_locale_currency" AS mloccu
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/locale/manager/currency/standard/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/currency/standard/insert/ansi
* mshop/locale/manager/currency/standard/update/ansi
* mshop/locale/manager/currency/standard/delete/ansi
* mshop/locale/manager/currency/standard/count/ansi

## standard/search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/currency/standard/search/mysql = 
 SELECT :columns
 	mloccu."id" AS "locale.currency.id", mloccu."label" AS "locale.currency.label",
 	mloccu."status" AS "locale.currency.status", mloccu."mtime" AS "locale.currency.mtime",
 	mloccu."editor" AS "locale.currency.editor", mloccu."ctime" AS "locale.currency.ctime"
 FROM "mshop_locale_currency" AS mloccu
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mloccu."id" AS "locale.currency.id", mloccu."label" AS "locale.currency.label",
 	mloccu."status" AS "locale.currency.status", mloccu."mtime" AS "locale.currency.mtime",
 	mloccu."editor" AS "locale.currency.editor", mloccu."ctime" AS "locale.currency.ctime"
 FROM "mshop_locale_currency" AS mloccu
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/locale/manager/currency/standard/search/ansi

## standard/update/ansi

Updates an existing currency record in the database

```
mshop/locale/manager/currency/standard/update/ansi = 
 UPDATE "mshop_locale_currency"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?
```

* Default: mshop/locale/manager/currency/standard/update
* Type: string - SQL statement for updating records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the currency item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the saveItems() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/currency/standard/insert/ansi
* mshop/locale/manager/currency/standard/delete/ansi
* mshop/locale/manager/currency/standard/search/ansi
* mshop/locale/manager/currency/standard/count/ansi

## standard/update/mysql

Updates an existing currency record in the database

```
mshop/locale/manager/currency/standard/update/mysql = 
 UPDATE "mshop_locale_currency"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?
```

* Default: 
 UPDATE "mshop_locale_currency"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?


See also:

* mshop/locale/manager/currency/standard/update/ansi

## submanagers

List of manager names that can be instantiated by the locale currency manager

```
mshop/locale/manager/currency/submanagers = Array
(
)
```

* Default: Array
* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


# decorators
## excludes

Excludes decorators added by the "common" option from the locale manager

```
mshop/locale/manager/decorators/excludes = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the locale manager.

```
 mshop/locale/manager/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the locale manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/decorators/global
* mshop/locale/manager/decorators/local

## global

Adds a list of globally available decorators only to the locale manager

```
mshop/locale/manager/decorators/global = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the locale manager.

```
 mshop/locale/manager/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the locale
manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/decorators/excludes
* mshop/locale/manager/decorators/local

## local

Adds a list of local decorators only to the locale manager

```
mshop/locale/manager/decorators/local = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Locale\Manager\Decorator\*") around the locale manager.

```
 mshop/locale/manager/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Locale\Manager\Decorator\Decorator2" only to the locale
manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/decorators/excludes
* mshop/locale/manager/decorators/global

# language
## decorators/excludes

Excludes decorators added by the "common" option from the locale language manager

```
mshop/locale/manager/language/decorators/excludes = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the locale language manager.

```
 mshop/locale/manager/language/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the locale language manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/language/decorators/global
* mshop/locale/manager/language/decorators/local

## decorators/global

Adds a list of globally available decorators only to the locale language manager

```
mshop/locale/manager/language/decorators/global = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the locale language
manager.

```
 mshop/locale/manager/language/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the locale
language manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/language/decorators/excludes
* mshop/locale/manager/language/decorators/local

## decorators/local

Adds a list of local decorators only to the locale language manager

```
mshop/locale/manager/language/decorators/local = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Locale\Manager\Language\Decorator\*") around the locale
language manager.

```
 mshop/locale/manager/language/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Locale\Manager\Language\Decorator\Decorator2" only to the
locale language manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/language/decorators/excludes
* mshop/locale/manager/language/decorators/global

## name

Class name of the used locale language manager implementation

```
mshop/locale/manager/language/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default locale language manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Locale\Manager\Language\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Locale\Manager\Language\Mylanguage
```

then you have to set the this configuration option:

```
 mshop/locale/manager/language/name = Mylanguage
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyLanguage"!


## standard/count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/language/standard/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocla."id"
 	FROM "mshop_locale_language" AS mlocla
 	WHERE :cond
 	ORDER BY mlocla."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/locale/manager/language/standard/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/language/standard/insert/ansi
* mshop/locale/manager/language/standard/update/ansi
* mshop/locale/manager/language/standard/delete/ansi
* mshop/locale/manager/language/standard/search/ansi

## standard/count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/language/standard/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocla."id"
 	FROM "mshop_locale_language" AS mlocla
 	WHERE :cond
 	ORDER BY mlocla."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocla."id"
 	FROM "mshop_locale_language" AS mlocla
 	WHERE :cond
 	ORDER BY mlocla."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/locale/manager/language/standard/count/ansi

## standard/delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/language/standard/delete/ansi = 
 DELETE FROM "mshop_locale_language" WHERE :cond
```

* Default: mshop/locale/manager/language/standard/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the language records specified by the given IDs from the
locale database. The records must be from the site that is configured
via the context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/language/standard/insert/ansi
* mshop/locale/manager/language/standard/update/ansi
* mshop/locale/manager/language/standard/search/ansi
* mshop/locale/manager/language/standard/count/ansi

## standard/delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/language/standard/delete/mysql = 
 DELETE FROM "mshop_locale_language" WHERE :cond
```

* Default: 
 DELETE FROM "mshop_locale_language" WHERE :cond


See also:

* mshop/locale/manager/language/standard/delete/ansi

## standard/insert/ansi

Inserts a new language record into the database table

```
mshop/locale/manager/language/standard/insert/ansi = 
 INSERT INTO "mshop_locale_language" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/locale/manager/language/standard/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the language item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the saveItems() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/language/standard/update/ansi
* mshop/locale/manager/language/standard/delete/ansi
* mshop/locale/manager/language/standard/search/ansi
* mshop/locale/manager/language/standard/count/ansi

## standard/insert/mysql

Inserts a new language record into the database table

```
mshop/locale/manager/language/standard/insert/mysql = 
 INSERT INTO "mshop_locale_language" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_locale_language" ( :names
 	"label", "status", "mtime", "editor", "id", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?
 )


See also:

* mshop/locale/manager/language/standard/insert/ansi

## standard/search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/language/standard/search/ansi = 
 SELECT :columns
 	mlocla."id" AS "locale.language.id", mlocla."label" AS "locale.language.label",
 	mlocla."status" AS "locale.language.status", mlocla."mtime" AS "locale.language.mtime",
 	mlocla."editor" AS "locale.language.editor", mlocla."ctime" AS "locale.language.ctime"
 FROM "mshop_locale_language" AS mlocla
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/locale/manager/language/standard/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/language/standard/insert/ansi
* mshop/locale/manager/language/standard/update/ansi
* mshop/locale/manager/language/standard/delete/ansi
* mshop/locale/manager/language/standard/count/ansi

## standard/search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/language/standard/search/mysql = 
 SELECT :columns
 	mlocla."id" AS "locale.language.id", mlocla."label" AS "locale.language.label",
 	mlocla."status" AS "locale.language.status", mlocla."mtime" AS "locale.language.mtime",
 	mlocla."editor" AS "locale.language.editor", mlocla."ctime" AS "locale.language.ctime"
 FROM "mshop_locale_language" AS mlocla
 WHERE :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mlocla."id" AS "locale.language.id", mlocla."label" AS "locale.language.label",
 	mlocla."status" AS "locale.language.status", mlocla."mtime" AS "locale.language.mtime",
 	mlocla."editor" AS "locale.language.editor", mlocla."ctime" AS "locale.language.ctime"
 FROM "mshop_locale_language" AS mlocla
 WHERE :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/locale/manager/language/standard/search/ansi

## standard/update/ansi

Updates an existing language record in the database

```
mshop/locale/manager/language/standard/update/ansi = 
 UPDATE "mshop_locale_language"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?
```

* Default: mshop/locale/manager/language/standard/update
* Type: string - SQL statement for updating records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the language item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the saveItems() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/language/standard/insert/ansi
* mshop/locale/manager/language/standard/delete/ansi
* mshop/locale/manager/language/standard/search/ansi
* mshop/locale/manager/language/standard/count/ansi

## standard/update/mysql

Updates an existing language record in the database

```
mshop/locale/manager/language/standard/update/mysql = 
 UPDATE "mshop_locale_language"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?
```

* Default: 
 UPDATE "mshop_locale_language"
 SET :names
 	"label" = ?, "status" = ?, "mtime" = ?, "editor" = ?
 WHERE "id" = ?


See also:

* mshop/locale/manager/language/standard/update/ansi

## submanagers

List of manager names that can be instantiated by the locale language manager

```
mshop/locale/manager/language/submanagers = Array
(
)
```

* Default: Array
* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


# name

Class name of the used locale manager implementation

```
mshop/locale/manager/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default manager can be replace by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Locale\Manager\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Locale\Manager\Mymanager
```

then you have to set the this configuration option:

```
 mshop/locale/manager/name = Mymanager
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MyManager"!


# site
## cleanup/admin/domains

List of mshop domains names whose items referring to the same site should be deleted as well

```
mshop/locale/manager/site/cleanup/admin/domains = Array
(
    [0] => job
    [1] => log
    [2] => cache
)
```

* Default: Array
* Type: array - List of domain names in lower case
* Since: 2014.03

As items for each domain can be stored in a separate database, the
site manager needs a list of domain names used to connect to the
correct database and to remove all items that belong the the deleted
site.

For each domain the cleanup will be done by the corresponding MAdmin
manager. To keep records for old sites in the database even if the
site was already deleted, you can configure a new list with the
domains removed you would like to keep, e.g. the "log" domain to
keep all log entries ever written.

See also:

* mshop/locale/manager/site/cleanup/shop/domains

## cleanup/shop/domains

List of madmin domains names whose items referring to the same site should be deleted as well

```
mshop/locale/manager/site/cleanup/shop/domains = Array
(
    [0] => attribute
    [1] => catalog
    [2] => coupon
    [3] => customer
    [4] => index
    [5] => media
    [6] => order
    [7] => plugin
    [8] => price
    [9] => product
    [10] => review
    [11] => tag
    [12] => service
    [13] => stock
    [14] => subscription
    [15] => supplier
    [16] => text
)
```

* Default: Array
* Type: array - List of domain names in lower case
* Since: 2014.03

As items for each domain can be stored in a separate database, the
site manager needs a list of domain names used to connect to the
correct database and to remove all items that belong the the deleted
site.

For each domain the cleanup will be done by the corresponding MShop
manager. To keep records for old sites in the database even if the
site was already deleted, you can configure a new list with the
domains removed you would like to keep, e.g. the "order" domain to
keep all orders ever placed.

See also:

* mshop/locale/manager/site/cleanup/admin/domains

## decorators/excludes

Excludes decorators added by the "common" option from the locale site manager

```
mshop/locale/manager/site/decorators/excludes = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to remove a decorator added via
"mshop/common/manager/decorators/default" before they are wrapped
around the locale site manager.

```
 mshop/locale/manager/site/decorators/excludes = array( 'decorator1' )
```

This would remove the decorator named "decorator1" from the list of
common decorators ("\Aimeos\MShop\Common\Manager\Decorator\*") added via
"mshop/common/manager/decorators/default" for the locale site manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/site/decorators/global
* mshop/locale/manager/site/decorators/local

## decorators/global

Adds a list of globally available decorators only to the locale site manager

```
mshop/locale/manager/site/decorators/global = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap global decorators
("\Aimeos\MShop\Common\Manager\Decorator\*") around the locale site
manager.

```
 mshop/locale/manager/site/decorators/global = array( 'decorator1' )
```

This would add the decorator named "decorator1" defined by
"\Aimeos\MShop\Common\Manager\Decorator\Decorator1" only to the locale
site manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/site/decorators/excludes
* mshop/locale/manager/site/decorators/local

## decorators/local

Adds a list of local decorators only to the locale site manager

```
mshop/locale/manager/site/decorators/local = Array
(
)
```

* Default: Array
* Type: array - List of decorator names
* Since: 2014.03

Decorators extend the functionality of a class by adding new aspects
(e.g. log what is currently done), executing the methods of the underlying
class only in certain conditions (e.g. only for logged in users) or
modify what is returned to the caller.

This option allows you to wrap local decorators
("\Aimeos\MShop\Locale\Manager\Site\Decorator\*") around the locale site
manager.

```
 mshop/locale/manager/site/decorators/local = array( 'decorator2' )
```

This would add the decorator named "decorator2" defined by
"\Aimeos\MShop\Locale\Manager\Site\Decorator\Decorator2" only to the
locale site manager.

See also:

* mshop/common/manager/decorators/default
* mshop/locale/manager/site/decorators/excludes
* mshop/locale/manager/site/decorators/global

## name

Class name of the used locale site manager implementation

```
mshop/locale/manager/site/name = Standard
```

* Default: Standard
* Type: string - Last part of the class name
* Since: 2014.03

Each default locale site manager can be replaced by an alternative imlementation.
To use this implementation, you have to set the last part of the class
name as configuration value so the manager factory knows which class it
has to instantiate.

For example, if the name of the default class is

```
 \Aimeos\MShop\Locale\Manager\Site\Standard
```

and you want to replace it with your own version named

```
 \Aimeos\MShop\Locale\Manager\Site\Mysite
```

then you have to set the this configuration option:

```
 mshop/locale/manager/site/name = Mysite
```

The value is the last part of your own class name and it's case sensitive,
so take care that the configuration value is exactly named like the last
part of the class name.

The allowed characters of the class name are A-Z, a-z and 0-9. No other
characters are possible! You should always start the last part of the class
name with an upper case character and continue only with lower case characters
or numbers. Avoid chamel case names like "MySite"!


## standard/count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/site/standard/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocsi."id"
 	FROM "mshop_locale_site" AS mlocsi
 	WHERE :cond
 	ORDER BY mlocsi."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/locale/manager/site/standard/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/site/standard/insert/ansi
* mshop/locale/manager/site/standard/update/ansi
* mshop/locale/manager/site/standard/delete/ansi
* mshop/locale/manager/site/standard/search/ansi
* mshop/locale/manager/site/standard/newid/ansi

## standard/count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/site/standard/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocsi."id"
 	FROM "mshop_locale_site" AS mlocsi
 	WHERE :cond
 	ORDER BY mlocsi."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mlocsi."id"
 	FROM "mshop_locale_site" AS mlocsi
 	WHERE :cond
 	ORDER BY mlocsi."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/locale/manager/site/standard/count/ansi

## standard/delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/site/standard/delete/ansi = 
 DELETE FROM "mshop_locale_site"
 WHERE :cond
```

* Default: mshop/locale/manager/site/standard/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the site records specified by the given IDs from the
locale database. The records must be from the site that is configured
via the context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/site/standard/insert/ansi
* mshop/locale/manager/site/standard/update/ansi
* mshop/locale/manager/site/standard/search/ansi
* mshop/locale/manager/site/standard/count/ansi
* mshop/locale/manager/site/standard/newid/ansi

## standard/delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/site/standard/delete/mysql = 
 DELETE FROM "mshop_locale_site"
 WHERE :cond
```

* Default: 
 DELETE FROM "mshop_locale_site"
 WHERE :cond


See also:

* mshop/locale/manager/site/standard/delete/ansi

## standard/insert/ansi

Inserts a new currency record into the database table

```
mshop/locale/manager/site/standard/insert/ansi = 
 INSERT INTO "mshop_locale_site" ( :names
 	"siteid", "code", "label", "config", "status", "editor",
 	"mtime", "ctime", "parentid", "level", "nleft", "nright"
 )
 SELECT :values
 	?, ?, ?, ?, ?, ?, ?, ?, 0, 0,
 	COALESCE( MAX("nright"), 0 ) + 1, COALESCE( MAX("nright"), 0 ) + 2
 FROM "mshop_locale_site"
```

* Default: mshop/locale/manager/site/standard/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the site item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the saveItems() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/site/standard/update/ansi
* mshop/locale/manager/site/standard/delete/ansi
* mshop/locale/manager/site/standard/search/ansi
* mshop/locale/manager/site/standard/count/ansi
* mshop/locale/manager/site/standard/newid/ansi

## standard/insert/mysql

Inserts a new currency record into the database table

```
mshop/locale/manager/site/standard/insert/mysql = 
 INSERT INTO "mshop_locale_site" ( :names
 	"siteid", "code", "label", "config", "status", "editor",
 	"mtime", "ctime", "parentid", "level", "nleft", "nright"
 )
 SELECT :values
 	?, ?, ?, ?, ?, ?, ?, ?, 0, 0,
 	COALESCE( MAX("nright"), 0 ) + 1, COALESCE( MAX("nright"), 0 ) + 2
 FROM "mshop_locale_site"
```

* Default: 
 INSERT INTO "mshop_locale_site" ( :names
 	"siteid", "code", "label", "config", "status", "editor",
 	"mtime", "ctime", "parentid", "level", "nleft", "nright"
 )
 SELECT :values
 	?, ?, ?, ?, ?, ?, ?, ?, 0, 0,
 	COALESCE( MAX("nright"), 0 ) + 1, COALESCE( MAX("nright"), 0 ) + 2
 FROM "mshop_locale_site"


See also:

* mshop/locale/manager/site/standard/insert/ansi

## standard/newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/locale/manager/site/standard/newid/ansi = 
```

* Default: 
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_matt_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_matt_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/locale/manager/site/standard/insert/ansi
* mshop/locale/manager/site/standard/update/ansi
* mshop/locale/manager/site/standard/delete/ansi
* mshop/locale/manager/site/standard/search/ansi
* mshop/locale/manager/site/standard/count/ansi

## standard/newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/locale/manager/site/standard/newid/mysql = 
```

* Default: 

See also:

* mshop/locale/manager/site/standard/newid/ansi

## standard/search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/site/standard/search/ansi = 
 SELECT :columns
 	mlocsi."id" AS "locale.site.id", mlocsi."siteid" AS "locale.site.siteid",
 	mlocsi."code" AS "locale.site.code", mlocsi."label" AS "locale.site.label",
 	mlocsi."config" AS "locale.site.config", mlocsi."status" AS "locale.site.status",
 	mlocsi."editor" AS "locale.site.editor", mlocsi."mtime" AS "locale.site.mtime",
 	mlocsi."ctime" AS "locale.site.ctime"
 FROM "mshop_locale_site" AS mlocsi
 WHERE mlocsi."level" = 0 AND :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/locale/manager/site/standard/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the attribute
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

As the records can normally be limited by criteria from sub-managers,
their tables must be joined in the SQL context. This is done by
using the "internaldeps" property from the definition of the ID
column of the sub-managers. These internal dependencies specify
the JOIN between the tables and the used columns for joining. The
":joins" placeholder is then replaced by the JOIN strings from
the sub-managers.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/site/standard/insert/ansi
* mshop/locale/manager/site/standard/update/ansi
* mshop/locale/manager/site/standard/delete/ansi
* mshop/locale/manager/site/standard/count/ansi
* mshop/locale/manager/site/standard/newid/ansi

## standard/search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/site/standard/search/mysql = 
 SELECT :columns
 	mlocsi."id" AS "locale.site.id", mlocsi."siteid" AS "locale.site.siteid",
 	mlocsi."code" AS "locale.site.code", mlocsi."label" AS "locale.site.label",
 	mlocsi."config" AS "locale.site.config", mlocsi."status" AS "locale.site.status",
 	mlocsi."editor" AS "locale.site.editor", mlocsi."mtime" AS "locale.site.mtime",
 	mlocsi."ctime" AS "locale.site.ctime"
 FROM "mshop_locale_site" AS mlocsi
 WHERE mlocsi."level" = 0 AND :cond
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mlocsi."id" AS "locale.site.id", mlocsi."siteid" AS "locale.site.siteid",
 	mlocsi."code" AS "locale.site.code", mlocsi."label" AS "locale.site.label",
 	mlocsi."config" AS "locale.site.config", mlocsi."status" AS "locale.site.status",
 	mlocsi."editor" AS "locale.site.editor", mlocsi."mtime" AS "locale.site.mtime",
 	mlocsi."ctime" AS "locale.site.ctime"
 FROM "mshop_locale_site" AS mlocsi
 WHERE mlocsi."level" = 0 AND :cond
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/locale/manager/site/standard/search/ansi

## standard/update/ansi

Updates an existing site record in the database

```
mshop/locale/manager/site/standard/update/ansi = 
 UPDATE "mshop_locale_site"
 SET :names
 	"siteid" = ?, "code" = ?, "label" = ?, "config" = ?, "status" = ?, "editor" = ?, "mtime" = ?
 WHERE id = ?
```

* Default: mshop/locale/manager/site/standard/update
* Type: string - SQL statement for updating records
* Since: 2014.03

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the site item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the saveItems() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/site/standard/insert/ansi
* mshop/locale/manager/site/standard/delete/ansi
* mshop/locale/manager/site/standard/search/ansi
* mshop/locale/manager/site/standard/count/ansi
* mshop/locale/manager/site/standard/newid/ansi

## standard/update/mysql

Updates an existing site record in the database

```
mshop/locale/manager/site/standard/update/mysql = 
 UPDATE "mshop_locale_site"
 SET :names
 	"siteid" = ?, "code" = ?, "label" = ?, "config" = ?, "status" = ?, "editor" = ?, "mtime" = ?
 WHERE id = ?
```

* Default: 
 UPDATE "mshop_locale_site"
 SET :names
 	"siteid" = ?, "code" = ?, "label" = ?, "config" = ?, "status" = ?, "editor" = ?, "mtime" = ?
 WHERE id = ?


See also:

* mshop/locale/manager/site/standard/update/ansi

## submanagers

List of manager names that can be instantiated by the locale site manager

```
mshop/locale/manager/site/submanagers = Array
(
)
```

* Default: Array
* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.


# standard
## count/ansi

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/standard/count/ansi = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloc."id"
 	FROM "mshop_locale" AS mloc
 	LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 	LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 	LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 	WHERE :cond
 	GROUP BY mloc."id"
 	ORDER BY mloc."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list
```

* Default: mshop/locale/manager/standard/count
* Type: string - SQL statement for counting items
* Since: 2014.03

Counts all records matched by the given criteria from the locale
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the statement can count all records from the
current site and the complete sub-tree of sites.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

Both, the strings for ":joins" and for ":cond" are the same as for
the "search" SQL statement.

Contrary to the "search" statement, it doesn't return any records
but instead the number of records that have been found. As counting
thousands of records can be a long running task, the maximum number
of counted records is limited for performance reasons.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/standard/insert/ansi
* mshop/locale/manager/standard/update/ansi
* mshop/locale/manager/standard/newid/ansi
* mshop/locale/manager/standard/delete/ansi
* mshop/locale/manager/standard/search/ansi

## count/mysql

Counts the number of records matched by the given criteria in the database

```
mshop/locale/manager/standard/count/mysql = 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloc."id"
 	FROM "mshop_locale" AS mloc
 	LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 	LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 	LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 	WHERE :cond
 	GROUP BY mloc."id"
 	ORDER BY mloc."id"
 	LIMIT 10000 OFFSET 0
 ) AS list
```

* Default: 
 SELECT COUNT(*) AS "count"
 FROM (
 	SELECT mloc."id"
 	FROM "mshop_locale" AS mloc
 	LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 	LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 	LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 	WHERE :cond
 	GROUP BY mloc."id"
 	ORDER BY mloc."id"
 	OFFSET 0 ROWS FETCH NEXT 10000 ROWS ONLY
 ) AS list


See also:

* mshop/locale/manager/standard/count/ansi

## delete/ansi

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/standard/delete/ansi = 
 DELETE FROM "mshop_locale"
 WHERE :cond AND siteid = ?
```

* Default: mshop/locale/manager/standard/delete
* Type: string - SQL statement for deleting items
* Since: 2014.03

Removes the records specified by the given IDs from the locale database.
The records must be from the site that is configured via the
context item.

The ":cond" placeholder is replaced by the name of the ID column and
the given ID or list of IDs while the site ID is bound to the question
mark.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/standard/insert/ansi
* mshop/locale/manager/standard/update/ansi
* mshop/locale/manager/standard/newid/ansi
* mshop/locale/manager/standard/search/ansi
* mshop/locale/manager/standard/count/ansi

## delete/mysql

Deletes the items matched by the given IDs from the database

```
mshop/locale/manager/standard/delete/mysql = 
 DELETE FROM "mshop_locale"
 WHERE :cond AND siteid = ?
```

* Default: 
 DELETE FROM "mshop_locale"
 WHERE :cond AND siteid = ?


See also:

* mshop/locale/manager/standard/delete/ansi

## insert/ansi

Inserts a new locale record into the database table

```
mshop/locale/manager/standard/insert/ansi = 
 INSERT INTO "mshop_locale" ( :names
 	"langid", "currencyid", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: mshop/locale/manager/standard/insert
* Type: string - SQL statement for inserting records
* Since: 2014.03

Items with no ID yet (i.e. the ID is NULL) will be created in
the database and the newly created ID retrieved afterwards
using the "newid" SQL statement.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the locale item to the statement before they are
sent to the database server. The number of question marks must
be the same as the number of columns listed in the INSERT
statement. The order of the columns must correspond to the
order in the saveItems() method, so the correct values are
bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/standard/update/ansi
* mshop/locale/manager/standard/newid/ansi
* mshop/locale/manager/standard/delete/ansi
* mshop/locale/manager/standard/search/ansi
* mshop/locale/manager/standard/count/ansi

## insert/mysql

Inserts a new locale record into the database table

```
mshop/locale/manager/standard/insert/mysql = 
 INSERT INTO "mshop_locale" ( :names
 	"langid", "currencyid", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?
 )
```

* Default: 
 INSERT INTO "mshop_locale" ( :names
 	"langid", "currencyid", "pos", "status",
 	"mtime", "editor", "siteid", "ctime"
 ) VALUES ( :values
 	?, ?, ?, ?, ?, ?, ?, ?
 )


See also:

* mshop/locale/manager/standard/insert/ansi

## newid/ansi

Retrieves the ID generated by the database when inserting a new record

```
mshop/locale/manager/standard/newid/ansi = mshop/locale/manager/standard/newid
```

* Default: mshop/locale/manager/standard/newid
* Type: string - SQL statement for retrieving the last inserted record ID
* Since: 2014.03

As soon as a new record is inserted into the database table,
the database server generates a new and unique identifier for
that record. This ID can be used for retrieving, updating and
deleting that specific record from the table again.

For MySQL:
```
 SELECT LAST_INSERT_ID()
For PostgreSQL:
 SELECT currval('seq_mloc_id')
For SQL Server:
 SELECT SCOPE_IDENTITY()
For Oracle:
 SELECT "seq_mloc_id".CURRVAL FROM DUAL
```

There's no way to retrive the new ID by a SQL statements that
fits for most database servers as they implement their own
specific way.

See also:

* mshop/locale/manager/standard/insert/ansi
* mshop/locale/manager/standard/update/ansi
* mshop/locale/manager/standard/delete/ansi
* mshop/locale/manager/standard/search/ansi
* mshop/locale/manager/standard/count/ansi

## newid/mysql

Retrieves the ID generated by the database when inserting a new record

```
mshop/locale/manager/standard/newid/mysql = SELECT LAST_INSERT_ID()
```

* Default: mshop/locale/manager/standard/newid

See also:

* mshop/locale/manager/standard/newid/ansi

## search/ansi

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/standard/search/ansi = 
 SELECT :columns
 	mloc."id" AS "locale.id", mloc."siteid" AS "locale.siteid",
 	mloc."langid" AS "locale.languageid", mloc."currencyid" AS "locale.currencyid",
 	mloc."pos" AS "locale.position", mloc."status" AS "locale.status",
 	mloc."mtime" AS "locale.mtime", mloc."editor" AS "locale.editor",
 	mloc."ctime" AS "locale.ctime"
 FROM "mshop_locale" AS mloc
 LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 WHERE :cond
 GROUP BY :columns :group
 	mloc."id", mloc."siteid", mloc."langid", mloc."currencyid", mloc."pos",
 	mloc."status", mloc."mtime", mloc."editor", mloc."ctime"
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY
```

* Default: mshop/locale/manager/standard/search
* Type: string - SQL statement for searching items
* Since: 2014.03

Fetches the records matched by the given criteria from the locale
database. The records must be from one of the sites that are
configured via the context item. If the current site is part of
a tree of sites, the SELECT statement can retrieve all records
from the current site and the complete sub-tree of sites.

To limit the records matched, conditions can be added to the given
criteria object. It can contain comparisons like column names that
must match specific values which can be combined by AND, OR or NOT
operators. The resulting string of SQL conditions replaces the
":cond" placeholder before the statement is sent to the database
server.

If the records that are retrieved should be ordered by one or more
columns, the generated string of column / sort direction pairs
replaces the ":order" placeholder. In case no ordering is required,
the complete ORDER BY part including the "/*-orderby*/.../*orderby-*/"
markers is removed to speed up retrieving the records. Columns of
sub-managers can also be used for ordering the result set but then
no index can be used.

The number of returned records can be limited and can start at any
number between the begining and the end of the result set. For that
the ":size" and ":start" placeholders are replaced by the
corresponding values from the criteria object. The default values
are 0 for the start and 100 for the size value.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/standard/insert/ansi
* mshop/locale/manager/standard/update/ansi
* mshop/locale/manager/standard/newid/ansi
* mshop/locale/manager/standard/delete/ansi
* mshop/locale/manager/standard/count/ansi

## search/mysql

Retrieves the records matched by the given criteria in the database

```
mshop/locale/manager/standard/search/mysql = 
 SELECT :columns
 	mloc."id" AS "locale.id", mloc."siteid" AS "locale.siteid",
 	mloc."langid" AS "locale.languageid", mloc."currencyid" AS "locale.currencyid",
 	mloc."pos" AS "locale.position", mloc."status" AS "locale.status",
 	mloc."mtime" AS "locale.mtime", mloc."editor" AS "locale.editor",
 	mloc."ctime" AS "locale.ctime"
 FROM "mshop_locale" AS mloc
 LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 WHERE :cond
 GROUP BY :group mloc."id"
 ORDER BY :order
 LIMIT :size OFFSET :start
```

* Default: 
 SELECT :columns
 	mloc."id" AS "locale.id", mloc."siteid" AS "locale.siteid",
 	mloc."langid" AS "locale.languageid", mloc."currencyid" AS "locale.currencyid",
 	mloc."pos" AS "locale.position", mloc."status" AS "locale.status",
 	mloc."mtime" AS "locale.mtime", mloc."editor" AS "locale.editor",
 	mloc."ctime" AS "locale.ctime"
 FROM "mshop_locale" AS mloc
 LEFT JOIN "mshop_locale_site" AS mlocsi ON (mloc."siteid" = mlocsi."siteid")
 LEFT JOIN "mshop_locale_language" AS mlocla ON (mloc."langid" = mlocla."id")
 LEFT JOIN "mshop_locale_currency" AS mloccu ON (mloc."currencyid" = mloccu."id")
 WHERE :cond
 GROUP BY :columns :group
 	mloc."id", mloc."siteid", mloc."langid", mloc."currencyid", mloc."pos",
 	mloc."status", mloc."mtime", mloc."editor", mloc."ctime"
 ORDER BY :order
 OFFSET :start ROWS FETCH NEXT :size ROWS ONLY


See also:

* mshop/locale/manager/standard/search/ansi

## update/ansi

Updates an existing locale record in the database

```
mshop/locale/manager/standard/update/ansi = 
 UPDATE "mshop_locale"
 SET :names
 	"langid" = ?, "currencyid" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" = ? AND "id" = ?
```

* Default: mshop/locale/manager/standard/update
* Type: string - SQL statement for updating records
* Since: 2014.03

Items which already have an ID (i.e. the ID is not NULL) will
be updated in the database.

The SQL statement must be a string suitable for being used as
prepared statement. It must include question marks for binding
the values from the locale item to the statement before they are
sent to the database server. The order of the columns must
correspond to the order in the saveItems() method, so the
correct values are bound to the columns.

The SQL statement should conform to the ANSI standard to be
compatible with most relational database systems. This also
includes using double quotes for table and column names.

See also:

* mshop/locale/manager/standard/insert/ansi
* mshop/locale/manager/standard/newid/ansi
* mshop/locale/manager/standard/delete/ansi
* mshop/locale/manager/standard/search/ansi
* mshop/locale/manager/standard/count/ansi

## update/mysql

Updates an existing locale record in the database

```
mshop/locale/manager/standard/update/mysql = 
 UPDATE "mshop_locale"
 SET :names
 	"langid" = ?, "currencyid" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" = ? AND "id" = ?
```

* Default: 
 UPDATE "mshop_locale"
 SET :names
 	"langid" = ?, "currencyid" = ?, "pos" = ?,
 	"status" = ?, "mtime" = ?, "editor" = ?
 WHERE "siteid" = ? AND "id" = ?


See also:

* mshop/locale/manager/standard/update/ansi

# submanagers

List of manager names that can be instantiated by the locale manager

```
mshop/locale/manager/submanagers = Array
(
    [0] => language
    [1] => currency
    [2] => site
)
```

* Default: Array
* Type: array - List of sub-manager names
* Since: 2014.03

Managers provide a generic interface to the underlying storage.
Each manager has or can have sub-managers caring about particular
aspects. Each of these sub-managers can be instantiated by its
parent manager using the getSubManager() method.

The search keys from sub-managers can be normally used in the
manager as well. It allows you to search for items of the manager
using the search keys of the sub-managers to further limit the
retrieved list of items.