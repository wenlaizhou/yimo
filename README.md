# yimo
#### **yimo project**
***
**database schema:**
```sql
drop database yimo;
create database yimo DEFAULT CHARACTER SET utf8;
use yimo;
create table user (
    id varchar(36) primary key,
    mobile varchar(16) not null unique,
    name nvarchar(16) unique,
    id_card varchar(32),
    pwd varchar(16),
    avatar varchar(32),
    qrcode varchar(1024),
    amount decimal,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index user_index on user(id, mobile, name, status);

create table vgroup (
    id varchar(36) primary key,
    name nvarchar(32),
    description nvarchar(1024),
    avatar varchar(32),
    join_agreement nvarchar(1024),
    owner varchar(36),
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index group_index on vgroup(id, name) comment '';

create table group_type (
    id varchar(36) primary key,
    name nvarchar(16),
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index group_type_index on group_type(id, name) comment '';

create table group_type_ref (
    id varchar(36) primary key,
    group_name nvarchar(32),
    group_type_id varchar(36),
    group_type_name nvarchar(16),
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index group_type_ref_index on group_type_ref(id, group_name, group_type_name, group_type_id) comment '';

create table group_users (
    id varchar(36) primary key,
    group_id varchar(36) not null,
    user_id varchar(36) not null,
    create_at datetime default now(),
    update_at datetime default now(),
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index group_users_index on group_users(group_id, user_id) comment '';

create table help (
    id varchar(36) primary key,
    name nvarchar(32),
    help_principle nvarchar(1024),
    min_user_count integer unsigned,
    max_user_count integer unsigned,
    description nvarchar(1024),
    group_id varchar(36),
    owner varchar(36),
    help_amount decimal,
    review_day integer unsigned,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index help_index on help(id, name, group_id, status) comment '';

create table help_order (
    id varchar(36) primary key,
    help_id varchar(36),
    helped_user_id varchar(36),
    help_user_id varchar(36),
    amount decimal,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index help_order_index on help_order(id, help_id, helped_user_id, status) comment '';

create table article (
    id varchar(36) primary key,
    title nvarchar(128) not null,
    content longtext default null,
    author_id varchar(36) default null,
    author_name nvarchar(16) default null,
    group_id varchar(36) default null,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index article_index on article(id, group_id, author_id, author_name, status) comment '';

create table post (
    id varchar(36) primary key,
    title nvarchar(128) not null,
    content longtext default null,
    author_id varchar(36) default null comment '匿名',
    author_name nvarchar(16) default null,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index post_index on post(id, author_id, author_name, status) comment '';

create table follow (
    id varchar(36) primary key,
    title nvarchar(128),
    content longtext,
    author_id varchar(36) default null comment '匿名',
    author_name nvarchar(16) default null,
    post_id varchar(36) default null,
    follow_id varchar(36) default null comment '评论盖楼',
    level integer unsigned default 1,
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index follow_index on follow(id, author_id, author_name, post_id, follow_id, status) comment '';

create table message (
    id varchar(36) primary key,
    title nvarchar(128),
    content longtext,
    from_id varchar(36) default null comment '匿名',
    from_name nvarchar(16) default null,
    to_id varchar(36),
    create_at datetime default now(),
    update_at datetime default now(),
    type tinyint default 1,
    status tinyint default 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8, comment '';

create index message_index on message(id, to_id, status) comment '';
```

