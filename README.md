This repo contains a docker compose project demoing how to start a wordpress
instance using the sqlite plugin.

To start it, simply run

```bash
git clone git@github.com:WordPress/sqlite-database-integration.git
docker compose up -d
open http://localhost:8080
docker compose logs -f
```

It also includes a bind mount `wp-content` locally to play with the sqlite db

```bash
$ sqlite3 wp-content/database/wordpress.db
SQLite version 3.37.0 2021-12-09 01:34:53
Enter ".help" for usage hints.
sqlite> .tables
wp_commentmeta         wp_postmeta            wp_termmeta
wp_comments            wp_posts               wp_terms
wp_links               wp_term_relationships  wp_usermeta
wp_options             wp_term_taxonomy       wp_users
sqlite> .schema wp_posts
CREATE TABLE wp_posts (
	ID  integer   NOT NULL  PRIMARY KEY AUTOINCREMENT ,
	post_author  integer   NOT NULL default '0',
	post_date   text NOT NULL default '0000-00-00 00:00:00',
	post_date_gmt   text NOT NULL default '0000-00-00 00:00:00',
	post_content  text NOT NULL,
	post_title  text NOT NULL,
	post_excerpt  text NOT NULL,
	post_status   text NOT NULL default 'publish',
	comment_status   text NOT NULL default 'open',
	ping_status   text NOT NULL default 'open',
	post_password   text NOT NULL default '',
	post_name   text NOT NULL default '',
	to_ping  text NOT NULL,
	pinged  text NOT NULL,
	post_modified   text NOT NULL default '0000-00-00 00:00:00',
	post_modified_gmt   text NOT NULL default '0000-00-00 00:00:00',
	post_content_filtered  text NOT NULL,
	post_parent  integer   NOT NULL default '0',
	guid   text NOT NULL default '',
	menu_order   integer NOT NULL default '0',
	post_type   text NOT NULL default 'post',
	post_mime_type   text NOT NULL default '',
	comment_count  integer NOT NULL default '0'
);
CREATE INDEX post_name ON wp_posts(post_name);
CREATE INDEX type_status_date ON wp_posts(post_type,post_status,post_date,ID);
CREATE INDEX post_parent ON wp_posts(post_parent);
CREATE INDEX post_author ON wp_posts(post_author);
sqlite>
```

enjoy :)
