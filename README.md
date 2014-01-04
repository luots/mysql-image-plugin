mysql-image-plugin
==================

Build
-----
	cmake .
	make && make install
	
	or
	
	gcc -O3  -g  -I/usr/include/mysql -I/usr/include/sys  -fPIC -shared -o libimage.so image.c
	sudo mv libimage.so /usr/lib/mysql/plugin/
	
Setup
-----
	mysql> create function image_check returns string soname 'libimage.so';
	Query OK, 0 rows affected (0.44 sec)

Test
----
	mysql> select image_check('/www/images/logo.png');
	
Plugin
------
	drop function image_check;
	drop function image_remove;
	drop function image_rename;
	drop function image_crc32;
	drop function image_move;
	
	create function image_check returns string soname 'libimage.so';
	create function image_remove returns string soname 'libimage.so';
	create function image_rename returns string soname 'libimage.so';
	create function image_crc32 returns string soname 'libimage.so';
	create function image_move returns string soname 'libimage.so';

Example 
-------	
	select image_check('/path/filename.ext');
	select image_remove('/path/filename.ext');
	select image_rename('/path/oldfile.ext','/path/newfile.ext');
	select image_crc32('/path/filename.ext');
	select image_move('/path/filename.ext','/path/to/newfile.ext');
