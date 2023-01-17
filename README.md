instagram clone using mysql





create database ig_clone;
use ig_clone;
create table users(
	id int auto_increment primary key,
    username varchar(255) unique not null,
    created_at timestamp default now()
);

insert into users(username) values
("Ronit"),
("Sam"),
("Rishi");

create table photos(
	id int auto_increment primary key,
    image_url varchar(255) not null,
    user_id int not null,
    created_at timestamp default now(),
    foreign key(user_id) references users(id)
);

insert into photos(image_url,user_id)values
('/asdf',1),
('/addf',2),
('/asef',2);

create table comments(
	id integer auto_increment primary key,
    comment_text varchar(255) not null,
    user_id int not null,
    photo_id int not null,
    created_at timestamp default now(),
    foreign key(user_id) references users(id),
    foreign key(photo_id) references photos(id)
);

insert into comments(comment_text,user_id,photo_id)values
('Hello',1,2),
('World',1,1);

create table likes(
	user_id int not null,
    photo_id int not null,
    created_at timestamp default now(),
	foreign key (user_id) references users(id),
    foreign key(photo_id) references photos(id),
	primary key(user_id,photo_id)
);

insert into likes(user_id,photo_id)values
(1,2),
(1,1);

create table follows(
	follower_id int not null,
    followee_id int not null,
    created_at timestamp default now(),
    foreign key(follower_id) references users(id),
    foreign key(followee_id) references users(id)
);

insert into follows(follower_id,followee_id)values
(1,2),
(1,3);

create table tags(
	id int auto_increment primary key,
    tag_name varchar(255) unique,
    created_at timestamp default now()
);

create table photo_tags(
	photo_id int not null,
    tag_id int not null,
    foreign key(photo_id) references photos(id),
    foreign key(tag_id) references tags(id),
    primary key(photo_id,tag_id)
);

insert into tags(tag_name)values
('heljfds'),
('hdsuhdu');

insert into photo_tags(photo_id,tag_id)values
(1,1),
(2,2);
